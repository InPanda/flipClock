/* * 翻牌时钟 * @author： 兔子先生 * @createDate: 2019-11-24 */
<template>
    <div class="FlipClock">
        <Flipper ref="flipper0" />
        <Flipper ref="flipper1" />
        <Flipper ref="flipper2" />
        <Flipper ref="flipper3" />
        <Flipper ref="flipper4" />
        <Flipper ref="flipper5" />
    </div>
</template>

<script>
    import Flipper from './Flipper';

    export default {
        name: 'FlipClock',
        data() {
            return {
                timer: null,
                flipObjs: [],
                visitTodayNum: [0, 0, 0, 0, 0, 0],
                visitOldNum: [0, 0, 0, 0, 0, 0],
            };
        },
        components: {
            Flipper,
        },
        methods: {
            num2array(num) {
                let arr = num.toString().split('');
                switch (arr.length) {
                    case 0:
                        arr.unshift(0, 0, 0, 0, 0, 0);
                        return arr;
                    case 1:
                        arr.unshift(0, 0, 0, 0, 0);
                        return arr;
                    case 2:
                        arr.unshift(0, 0, 0, 0);
                        return arr;
                    case 3:
                        arr.unshift(0, 0, 0);
                        return arr;
                    case 4:
                        arr.unshift(0, 0);
                        return arr;
                    case 5:
                        arr.unshift(0);
                        return arr;
                    case 6:
                        return arr;
                }
            },
            init1() {
                for (let i = 0; i < this.visitTodayNum.length; i++) {
                    this.$nextTick(() => {
                        this.flipObjs[i].setFront(this.visitTodayNum[i]);
                    });
                }
            },
            run1() {
                this.timer = setInterval(() => {
                    // 获取当前时间
                    this.visitOldNum = this.visitTodayNum;
                    let now = Math.floor(Math.random() * 100);
                    this.visitTodayNum = this.num2array(now);
                    for (let i = 0; i < this.flipObjs.length; i++) {
                        if (this.visitOldNum[i] === this.visitTodayNum[i]) {
                            continue;
                        }
                        this.flipObjs[i].flipDown(this.visitOldNum[i], this.visitTodayNum[i]);
                    }
                }, 3000);
            },
        },
        mounted() {
            this.flipObjs = [this.$refs.flipper0, this.$refs.flipper1, this.$refs.flipper2, this.$refs.flipper3, this.$refs.flipper4, this.$refs.flipper5];
            this.init1();
            this.run1();
        },
    };
</script>

<style>
    .FlipClock {
        text-align: center;
    }
    .FlipClock .M-Flipper {
        margin: 0 3px;
    }
    .FlipClock em {
        display: inline-block;
        line-height: 102px;
        font-size: 66px;
        font-style: normal;
        vertical-align: top;
    }
</style>
