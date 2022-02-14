<template>
  <div class="wrapper-popup" v-bind:class="getClassPopup">
        <div class="rule">
            <h3>Luật chơi</h3>
            <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Totam quam repellendus voluptas fugit, rerum odit voluptatum qui ad voluptates ex accusamus optio maxime voluptatem dolorum nihil provident ab quidem temporibus.</p>
            <button v-on:click="confirmPlaying">Đã hiểu</button>
        </div>
  </div>
</template>

<script>
export default {
    name: 'popup-rule',
    props: {
        isOpenPopup: {
            type: Boolean,
            default: false
        }
    },
    data() {
        return {}
    },
    methods: {
        confirmPlaying() {
            this.$emit('handleConfirmPlaying')
        }
    },
    computed: {
        getClassPopup() {
            return {
                open: this.isOpenPopup
            }
        }
    }

}
</script>

<style>
.wrapper-popup {
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    background-color: rgba(0,0,0,0.4);
    opacity: 0;
    visibility: hidden;
}

.wrapper-popup.open {
    opacity: 1;
    visibility: visible;
}

.rule {
    background-color: #fff;
    width: 350px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%) scale(1.2);
    padding: 10px 15px;
    font-family: Arial, Helvetica, sans-serif;
    transition: all 0.3s ease;
}

.rule h3 {
    margin-bottom: 10px;
}

.open .rule {
    transform: translate(-50%, -50%) scale(1);
}

.rule button {
    margin-top: 20px;
    border: 2px solid #333;
    background-color: #fff;
    padding: 8px 15px;
}

.rule button:hover {
    cursor: pointer;
    background-color: #333;
    color: #fff;
}

</style>