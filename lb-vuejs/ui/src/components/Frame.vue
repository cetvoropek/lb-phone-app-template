<template>
    <div class="phone-frame">
        <div className="phone-time">{{ time }}</div>
        <div className="phone-notch"></div>
        <div className="phone-indicator"></div>
        <div class="phone-content">
            <slot />
        </div>
    </div>
</template>

<script>
export default {
    name: 'Frame',
    data() {
        return {
            time: '00:00'
        };
    },
    mounted() {
        this.updateTime(); // Initialize time on mount
        this.interval = setInterval(this.updateTime, 1000);
    },
    beforeDestroy() {
        clearInterval(this.interval);
    },
    methods: {
        updateTime() {
            const date = new Date();
            const hours = date.getHours().toString().padStart(2, '0');
            const minutes = date.getMinutes().toString().padStart(2, '0');
            this.time = `${hours}:${minutes}`;
        }
    }
};
</script>

<style scoped>
.phone-frame {
    position: absolute;
    z-index: 0;

    width: 92%;
    height: 98%;

    border-radius: 60px;
    box-shadow: 0 0 0.1em 0.25em #050506, 0 0 0 0.4em hsl(254, 30%, 85%);
}

.phone-content {
    height: 100%;
    width: 100%;

    display: flex;
    align-items: center;
    justify-content: center;

    overflow: hidden;
    border-radius: 60px;
}

.phone-notch {
    position: absolute;
    top: 0.75rem;
    left: 50%;
    transform: translateX(-50%);

    height: 2.25rem;

    width: 30%;
    background-color: black;

    border-radius: 25px;
    cursor: pointer;
}

.phone-indicator {
    position: absolute;

    left: 0;
    right: 0;
    bottom: 0.5rem;
    margin: auto;

    width: 9rem;
    height: 0.313rem;

    z-index: 999;

    display: flex;
    align-items: center;
    justify-content: center;

    border-radius: 0.25rem;

    background: transparent;
    backdrop-filter: grayscale(1) invert(1) contrast(100);

    cursor: pointer;
}

.phone-time {
    position: absolute;
    top: 0;
    width: 100%;

    padding: 1.2rem 3.5rem;

    z-index: 9;

    pointer-events: none;

    font-weight: 500;
    font-size: 1rem;

    color: black;

    font-family: 'Poppins', sans-serif;
}
</style>
