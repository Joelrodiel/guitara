<template>
    <div class="card center">
        <div class="bgIMG">
            <label v-for="(s, i) in strings" :key="'str'+i" class="papaS">
                <input type="checkbox" class="string"
                    v-on:click="changeString(i)">
                <span class="string"></span>
            </label>
            <div class="spacer"></div>
            <div v-for="j in 7" :key="j" class="looper">
                <label v-for="i in 6" :key="i" class="papa">
                    <input type="checkbox" class="select"
                        :id="'note_' + ((i-1) + (6*(j-1)))" v-on:click="addNote((i-1) + (6*(j-1)))">
                    <span class="select"></span>
                </label>
            </div>
        </div>
        <button class="button btn-left" v-on:click="uncheckAll">X</button>
        <button class="button">--</button>
        <button class="button btn-right">O</button>
    </div>
</template>

<script>
export default {
    name: 'Chord',
    data: function () {
        var notes = [];
        var strings = [];
        for (var i = 0; i < 7 * 6; i++) {
            notes[i] = false;
            if (i < 6) {
                strings[i] = true;
            }
        }
        return {
            notes: notes,
            strings: strings
        }
    },
    methods: {
        addNote(num) {
            for (var i = num % 6; i < 7*6; i += 6) {
                if (i != num) {
                    var id = 'note_' + i;
                    document.getElementById(id).checked = false;
                    this.notes[i] = false;
                }
            }
            this.notes[num] = !this.notes[num];
        },
        changeString(num) {
            this.strings[num] = !this.strings[num];
        },
        uncheckAll() {
            var checkboxes = new Array();
            checkboxes = document.getElementsByClassName('select');

            for (var i = 0; i < checkboxes.length; i++) {
                if (checkboxes[i].type == 'checkbox') {
                    checkboxes[i].checked = false;
                }
            }
            for (var k = 0; k < 7 * 6; k++) {
                this.notes[k] = false;
            }
            
            checkboxes = document.getElementsByClassName('string');
            for (i = 0; i < checkboxes.length; i++) {
                if (checkboxes[i].type == 'checkbox') {
                    checkboxes[i].checked = false;
                }
            }
            for (k = 0; k < 6; k++) {
                this.strings[k] = true;
            }
        }
    }
}
</script>

<style scoped>
.center {
    position: fixed;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
}
.card {
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  transition: 0.3s;
  border-radius: 8px;
  background-color: white;
}
.bgIMG {
    background-image: url("../assets/chordsBG.png");
    width: 306px;
    height: 497px;
    image-rendering: pixelated;
    image-rendering: -moz-crisp-edges;
    image-rendering: crisp-edges;
    margin: 20px 10px 20px 10px;
    user-select: none;
    -moz-user-select: none;
    -webkit-user-drag: none;
    -webkit-user-select: none;
}
.button {
    background-color: #ECF0F1;
    border: none;
    color: #98A0A5;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    width: 33.33%;
    font-size: 20px;
}
.btn-left {
    border-bottom-left-radius: 8px;
}
.btn-right {
    border-bottom-right-radius: 8px;
}
.spacer {
    height: 47.5px;
}
.looper {
    margin: 0;
    box-sizing: border-box;
    -moz-box-sizing: border-box;
    -webkit-box-sizing: border-box;
    font-size: 0px;
}
.looper input {
    position: absolute;
    cursor: pointer;
    margin: 0;
}
.papa {
    position: relative;
    width: 50px;
    height: 64.286px;
    margin: 0;
    float: left;
}
.papa .select {
    position: absolute;
    top: 0;
    left: 0;
    background-color: black;
    opacity: 0;
    margin: 0;
    width: 30px;
    height: 30px;
    transform: translate(12px, 12px);
    border-radius: 50%;
}
.papa input:checked ~ .select {
    opacity: 100%;
}
.papaS {
    position: relative;
    width: 50px;
    height: 32.143px;
    margin: 0;
    float: left;
}
.papaS input {
    opacity: 0;
}
.papaS .string {
    position: absolute;
    top: 0;
    left: 0;
    margin: 0;
    width: 24px;
    height: 24px;
    transform: translate(17px, 0);
    background-image: url("../assets/ou.png");
    image-rendering: auto;
}
.papaS input:checked ~ .string {
    background-image: url("../assets/cross.png");
}
</style>