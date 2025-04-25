# Binary-search-
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Binary Search with Vue</title>
  <script src="https://unpkg.com/vue@3"></script>
  <style>
    body { font-family: sans-serif; padding: 20px; }
    .array-box { display: flex; gap: 10px; margin-top: 10px; }
    .item {
      padding: 10px 15px;
      border: 1px solid #ccc;
      border-radius: 4px;
      background-color: #f5f5f5;
    }
    .highlight { background-color: #87cefa; font-weight: bold; }
  </style>
</head>
<body>
  <div id="app">
    <h2>二分查找可视化</h2>
    <p>数组：{{ numbers.join(", ") }}</p>
    <input type="number" v-model.number="target" placeholder="输入要查找的数字">
    <button @click="binarySearch">开始查找</button>

    <div class="array-box">
      <div v-for="(num, index) in numbers"
           :key="index"
           :class="['item', index === mid ? 'highlight' : '']">
        {{ num }}
      </div>
    </div>

    <p v-if="result !== null">结果：{{ result }}</p>
  </div>

  <script>
    const { createApp } = Vue;
    createApp({
      data() {
        return {
          numbers: [1, 3, 5, 7, 9, 11, 13, 15, 17, 19],
          target: null,
          mid: null,
          result: null
        };
      },
      methods: {
        binarySearch() {
          let left = 0;
          let right = this.numbers.length - 1;
          this.result = null;

          const interval = setInterval(() => {
            if (left > right) {
              clearInterval(interval);
              this.mid = null;
              this.result = '未找到';
              return;
            }

            this.mid = Math.floor((left + right) / 2);
            const guess = this.numbers[this.mid];

            if (guess === this.target) {
              this.result = `找到了！索引是 ${this.mid}`;
              clearInterval(interval);
            } else if (guess > this.target) {
              right = this.mid - 1;
            } else {
              left = this.mid + 1;
            }
          }, 800); // 每800毫秒更新一次，让可视化更明显
        }
      }
    }).mount('#app');
  </script>
</body>
</html>
