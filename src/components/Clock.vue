<template>
    <div class="clock">
        <div
            class="hours"
            :style="{transform:`rotate(${hoursRotate}deg)`}"
        ></div>
        <div
            class="minutes"
            :style="{transform:`rotate(${minutesRotate}deg)`}"
        ></div>
        <div
            class="seconds"
            :style="{transform:`rotate(${secondsRotate}deg)`}"
        ></div>
        <div class="center">
        </div>
        <div
            v-for="n in 60"
            :key="n"
            class="dimension"
            :style="{transform:`rotate(${n*6}deg)`}"
        >
            <span
                v-if="n%5==0"
                :class="[n/5===6?'six' : '']"
            >{{n/5}}</span>
        </div>
    </div>
</template>

<script>
/* eslint-disable */
export default {
    name: 'Clock',
    data () {
        return {
            hoursRotate: 0,
            minutesRotate: 0,
            secondsRotate: 0
        }
    },
    mounted () {
        const updateAngle = () => {
            let date = new Date();
            let hours = date.getHours() % 12;
            let minutes = date.getMinutes();
            let seconds = date.getSeconds();
            let secondsAngle = seconds * 6;
            let minutesAngle = (minutes * 6) + (secondsAngle / 60);
            let hoursAngle = (hours * 30) + (minutesAngle / 60);
            this.secondsRotate = secondsAngle;
            this.minutesRotate = minutesAngle;
            this.hoursRotate = hoursAngle;
            requestAnimationFrame(updateAngle);
        }
        requestAnimationFrame(updateAngle)
        // updateAngle();
        // var timeSecondsID = setInterval(updateAngle, 1000);
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang='less'>
.clock {
    width: 500px;
    height: 500px;
    border-radius: 50%;
    border: 20px solid #fae000;
    margin: 0 auto;
    position: relative;
    box-shadow: inset 0 0 0px 12px #f8b101;
}
.six {
    transform: rotate(180deg);
}
.hours {
    position: absolute;
    bottom: 50%;
    left: 50%;
    margin-left: -5px;
    transform-origin: 50% 100%;
    width: 10px;
    height: 100px;
    background: #10b7ee;
}
.minutes {
    position: absolute;
    bottom: 50%;
    left: 50%;
    margin-left: -4px;
    transform-origin: 50% 100%;
    width: 8px;
    height: 140px;
    background: #10b7ee;
}
.seconds {
    position: absolute;
    bottom: 50%;
    left: 50%;
    margin-left: -3px;
    transform-origin: 50% 100%;
    width: 6px;
    height: 165px;
    background: #ee0a15;
    &::before {
        content: "";
        position: absolute;
        top: 0;
        left: 0;
        border-bottom: 15px solid#ee0a15;
        border-right: 10px solid transparent;
        border-left: 10px solid transparent;
        margin-top: -10px;
        margin-left: -7px;
    }
}
.center {
    position: absolute;
    top: 50%;
    left: 50%;
    background: #ffdd02;
    width: 26px;
    height: 26px;
    margin-left: -13px;
    margin-top: -13px;
    border-radius: 50%;
    box-shadow: 0 0 0 5px #c0ee0a inset, 0 0 0 5px #ee0a15;
}
.dimension {
    // background: #a3a3a3;
    height: 50%;
    width: 5px;
    bottom: 50%;
    left: 50%;
    position: absolute;
    margin-left: -3px;
    margin-top: -3px;
    transform-origin: 50% 100%;
    span {
        position: absolute;
        margin-left: -17px;
        top: 15%;
        font-size: 30px;
        display: inline-block;
        width: 40px;
        text-align: center;
    }
    &::after {
        content: "";
        position: absolute;
        top: 8%;
        left: 0;
        height: 5px;
        width: 5px;
        background: #a3a3a3;
        border-radius: 50%;
    }
    &:nth-child(5n-1) {
        &::after {
            height: 25px;
            width: 5px;
            background: #242321;
            border-radius: 0;
            top: 4.5%;
        }
    }
}
</style>
