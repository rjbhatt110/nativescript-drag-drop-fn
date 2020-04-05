<template>
  <Page>
    <ActionBar title="Drag and Drop Nativescript"/>
    <GridLayout
      ref="grid"
      rows="auto, auto"
      columns="auto,auto"
      verticalAlignment="top"
      horizontalAlignment="center"
    >
      <Image ref="box0" src="res://droparea" row="0" col="0" class="box" />
      <Image ref="box1" src="res://droparea" row="0" col="1" class="box" />
      <Image ref="box2" src="res://droparea" row="1" col="0" class="box" />
      <Image ref="box3" src="res://droparea" row="1" col="1" class="box" />
      <Image
        v-for="(drag, index) in boxArray"
        :key="drag.refId"
        :ref="index"
        :src="drag.src"
        :row="drag.row"
        :col="drag.col"
        class="solid"
        @pan="onPan($event, index, drag)"
      />
    </GridLayout>
  </Page>
</template>

<script>
import { PanGestureEventData } from "ui/gestures";

export default {
  name: "Home",
  data() {
    return {
      boxArray: [
        {
          refId: "drag0",
          row: 0,
          col: 0,
          src: "res://dragbox1",
        },
        {
          refId: "drag1",
          row: 0,
          col: 1,
          src: "res://dragbox2",
        },
        {
          refId: "drag2",
          row: 1,
          col: 0,
          src: "res://dragbox3",
        },
        {
          refId: "drag3",
          row: 1,
          col: 1,
          src: "res://dragbox4",
        },
      ],
    };
  },
  computed: {},
  created() {},
  mounted() {
    this.box0 = this.$refs.box0.nativeView;
    this.box1 = this.$refs.box1.nativeView;
    this.box2 = this.$refs.box2.nativeView;
    this.box3 = this.$refs.box3.nativeView;
  },
  methods: {
    onPan(args, ref, box) {
      // Down
      if (args.state === 1) {
        this.prevDeltaX = 0;
        this.prevDeltaY = 0;
        this.translateX = this.$refs[ref][0].nativeView.translateX;
        this.translateY = this.$refs[ref][0].nativeView.translateY;
        // Panning Start
      } else if (args.state === 2) {
        // Panning logic for draging objects.
        this.$refs[ref][0].nativeView.translateX +=
          args.deltaX - this.prevDeltaX;
        this.$refs[ref][0].nativeView.translateY +=
          args.deltaY - this.prevDeltaY;
        this.prevDeltaX = args.deltaX;
        this.prevDeltaY = args.deltaY;
        // Drop Area animation whenever Object pass over from.
        if (
          this.$refs[ref][0].nativeView.getLocationOnScreen().x >=
            this.box0.getLocationOnScreen().x &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().x <=
            this.box0.getLocationOnScreen().x + this.box0.width &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y >=
            this.box0.getLocationOnScreen().y &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y <=
            this.box0.getLocationOnScreen().y + this.box0.height
        ) {
          this.box0.scaleX = 1.1;
          this.box0.scaleY = 1.1;
        } else {
          this.box0.scaleX = 1;
          this.box0.scaleY = 1;
        }

        if (
          this.$refs[ref][0].nativeView.getLocationOnScreen().x >=
            this.box1.getLocationOnScreen().x &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().x <=
            this.box1.getLocationOnScreen().x + this.box1.width &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y >=
            this.box1.getLocationOnScreen().y &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y <=
            this.box1.getLocationOnScreen().y + this.box1.height
        ) {
          this.box1.scaleX = 1.1;
          this.box1.scaleY = 1.1;
        } else {
          this.box1.scaleX = 1;
          this.box1.scaleY = 1;
        }

        if (
          this.$refs[ref][0].nativeView.getLocationOnScreen().x >=
            this.box2.getLocationOnScreen().x &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().x <=
            this.box2.getLocationOnScreen().x + this.box2.width &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y >=
            this.box2.getLocationOnScreen().y &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y <=
            this.box2.getLocationOnScreen().y + this.box2.height
        ) {
          this.box2.scaleX = 1.1;
          this.box2.scaleY = 1.1;
        } else {
          this.box2.scaleX = 1;
          this.box2.scaleY = 1;
        }

        if (
          this.$refs[ref][0].nativeView.getLocationOnScreen().x >=
            this.box3.getLocationOnScreen().x &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().x <=
            this.box3.getLocationOnScreen().x + this.box3.width &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y >=
            this.box3.getLocationOnScreen().y &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y <=
            this.box3.getLocationOnScreen().y + this.box3.height
        ) {
          this.box3.scaleX = 1.1;
          this.box3.scaleY = 1.1;
        } else {
          this.box3.scaleX = 1;
          this.box3.scaleY = 1;
        }
        // UP
      } else if (args.state === 3) {
        if (
          // <========== BOX 0 ===========>
          this.$refs[ref][0].nativeView.getLocationOnScreen().x >=
            this.box0.getLocationOnScreen().x &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().x <=
            this.box0.getLocationOnScreen().x + this.box0.width &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y >=
            this.box0.getLocationOnScreen().y &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y <=
            this.box0.getLocationOnScreen().y + this.box0.height
        ) {
          this.translateX = this.$refs[ref][0].nativeView.translateX;
          this.translateY = this.$refs[ref][0].nativeView.translateY;
          this.box0.scaleX = 1;
          this.box0.scaleY = 1;

          if (this.$refs[ref][0].nativeView.translateX >= -30) {
            this.$refs[ref][0].nativeView.translateX = 0;
          } else {
            this.$refs[ref][0].nativeView.translateX = -160;
          }
          if (this.$refs[ref][0].nativeView.translateY >= -30) {
            this.$refs[ref][0].nativeView.translateY = 0;
          } else {
            this.$refs[ref][0].nativeView.translateY = -140;
          }
          // Translate Animation Start 0
          // Handle Animation for swipe object from different position
          switch (ref) {
            case 1:
              if (
                this.$refs[this.boxArray.indexOf(this.boxArray[0])][0]
                  .nativeView.translateX >= 0
              ) {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[0])
                ][0].nativeView.translateX =
                  160 -
                  this.$refs[this.boxArray.indexOf(this.boxArray[0])][0]
                    .nativeView.translateX;
              } else {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[0])
                ][0].nativeView.translateX =
                  160 +
                  this.$refs[this.boxArray.indexOf(this.boxArray[0])][0]
                    .nativeView.translateX;
              }
              if (
                this.$refs[this.boxArray.indexOf(this.boxArray[0])][0]
                  .nativeView.translateY >= 0
              ) {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[0])
                ][0].nativeView.translateY =
                  0 -
                  this.$refs[this.boxArray.indexOf(this.boxArray[0])][0]
                    .nativeView.translateY;
              } else {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[0])
                ][0].nativeView.translateY =
                  0 +
                  this.$refs[this.boxArray.indexOf(this.boxArray[0])][0]
                    .nativeView.translateY;
              }
              break;
            case 2:
              if (
                this.$refs[this.boxArray.indexOf(this.boxArray[0])][0]
                  .nativeView.translateX >= 0
              ) {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[0])
                ][0].nativeView.translateX =
                  0 -
                  this.$refs[this.boxArray.indexOf(this.boxArray[0])][0]
                    .nativeView.translateX;
              } else {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[0])
                ][0].nativeView.translateX =
                  0 +
                  this.$refs[this.boxArray.indexOf(this.boxArray[0])][0]
                    .nativeView.translateX;
              }
              if (
                this.$refs[this.boxArray.indexOf(this.boxArray[0])][0]
                  .nativeView.translateY >= 0
              ) {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[0])
                ][0].nativeView.translateY =
                  140 -
                  this.$refs[this.boxArray.indexOf(this.boxArray[0])][0]
                    .nativeView.translateY;
              } else {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[0])
                ][0].nativeView.translateY =
                  140 +
                  this.$refs[this.boxArray.indexOf(this.boxArray[0])][0]
                    .nativeView.translateY;
              }
              break;
            case 3:
              if (
                this.$refs[this.boxArray.indexOf(this.boxArray[0])][0]
                  .nativeView.translateX >= 0
              ) {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[0])
                ][0].nativeView.translateX =
                  160 -
                  this.$refs[this.boxArray.indexOf(this.boxArray[0])][0]
                    .nativeView.translateX;
              } else {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[0])
                ][0].nativeView.translateX =
                  160 +
                  this.$refs[this.boxArray.indexOf(this.boxArray[0])][0]
                    .nativeView.translateX;
              }
              if (
                this.$refs[this.boxArray.indexOf(this.boxArray[0])][0]
                  .nativeView.translateY >= 0
              ) {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[0])
                ][0].nativeView.translateY =
                  140 -
                  this.$refs[this.boxArray.indexOf(this.boxArray[0])][0]
                    .nativeView.translateY;
              } else {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[0])
                ][0].nativeView.translateY =
                  140 +
                  this.$refs[this.boxArray.indexOf(this.boxArray[0])][0]
                    .nativeView.translateY;
              }
              break;
          }
          // Translate Animation End 0
          // Array that control Position drag item
          this.boxArray.splice(ref, 1, this.boxArray[0]);
          this.boxArray.splice(0, 1, box);
        } else if (
          // <========== BOX 1 ===========>
          this.$refs[ref][0].nativeView.getLocationOnScreen().x >=
            this.box1.getLocationOnScreen().x &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().x <=
            this.box1.getLocationOnScreen().x + this.box1.width &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y >=
            this.box1.getLocationOnScreen().y &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y <=
            this.box1.getLocationOnScreen().y + this.box1.height
        ) {
          this.translateX = this.$refs[ref][0].nativeView.translateX;
          this.translateY = this.$refs[ref][0].nativeView.translateY;
          this.box1.scaleX = 1;
          this.box1.scaleY = 1;
          if (this.$refs[ref][0].nativeView.translateX >= 140) {
            this.$refs[ref][0].nativeView.translateX = 160;
          } else {
            this.$refs[ref][0].nativeView.translateX = 0;
          }
          if (this.$refs[ref][0].nativeView.translateY >= -30) {
            this.$refs[ref][0].nativeView.translateY = 0;
          } else {
            this.$refs[ref][0].nativeView.translateY = -140;
          }
          // Translate Animation Start 1
          // Handle Animation for swipe object from different position
          switch (ref) {
            case 0:
              if (
                this.$refs[this.boxArray.indexOf(this.boxArray[1])][0]
                  .nativeView.translateX >= 0
              ) {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[1])
                ][0].nativeView.translateX =
                  this.$refs[this.boxArray.indexOf(this.boxArray[1])][0]
                    .nativeView.translateX - 160;
              } else {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[1])
                ][0].nativeView.translateX =
                  this.$refs[this.boxArray.indexOf(this.boxArray[1])][0]
                    .nativeView.translateX - 160;
              }
              if (
                this.$refs[this.boxArray.indexOf(this.boxArray[1])][0]
                  .nativeView.translateY >= 0
              ) {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[1])
                ][0].nativeView.translateY =
                  this.$refs[this.boxArray.indexOf(this.boxArray[1])][0]
                    .nativeView.translateY - 0;
              } else {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[1])
                ][0].nativeView.translateY =
                  this.$refs[this.boxArray.indexOf(this.boxArray[1])][0]
                    .nativeView.translateY + 0;
              }
              break;
            case 2:
              if (
                this.$refs[this.boxArray.indexOf(this.boxArray[1])][0]
                  .nativeView.translateX >= 0
              ) {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[1])
                ][0].nativeView.translateX =
                  this.$refs[this.boxArray.indexOf(this.boxArray[1])][0]
                    .nativeView.translateX - 160;
              } else {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[1])
                ][0].nativeView.translateX =
                  this.$refs[this.boxArray.indexOf(this.boxArray[1])][0]
                    .nativeView.translateX - 160;
              }
              if (
                this.$refs[this.boxArray.indexOf(this.boxArray[1])][0]
                  .nativeView.translateY >= 0
              ) {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[1])
                ][0].nativeView.translateY =
                  140 -
                  this.$refs[this.boxArray.indexOf(this.boxArray[1])][0]
                    .nativeView.translateY;
              } else {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[1])
                ][0].nativeView.translateY =
                  140 +
                  this.$refs[this.boxArray.indexOf(this.boxArray[1])][0]
                    .nativeView.translateY;
              }
              break;
            case 3:
              if (
                this.$refs[this.boxArray.indexOf(this.boxArray[1])][0]
                  .nativeView.translateX >= 0
              ) {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[1])
                ][0].nativeView.translateX =
                  this.$refs[this.boxArray.indexOf(this.boxArray[1])][0]
                    .nativeView.translateX - 0;
              } else {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[1])
                ][0].nativeView.translateX =
                  this.$refs[this.boxArray.indexOf(this.boxArray[1])][0]
                    .nativeView.translateX + 0;
              }
              if (
                this.$refs[this.boxArray.indexOf(this.boxArray[1])][0]
                  .nativeView.translateY >= 0
              ) {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[1])
                ][0].nativeView.translateY =
                  140 -
                  this.$refs[this.boxArray.indexOf(this.boxArray[1])][0]
                    .nativeView.translateY;
              } else {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[1])
                ][0].nativeView.translateY =
                  140 +
                  this.$refs[this.boxArray.indexOf(this.boxArray[1])][0]
                    .nativeView.translateY;
              }
              break;
          }
          // Translate Animation End 1
          // Array that control Position drag item
          this.boxArray.splice(ref, 1, this.boxArray[1]);
          this.boxArray.splice(1, 1, box);
        } else if (
          // <========== BOX 2 ===========>
          this.$refs[ref][0].nativeView.getLocationOnScreen().x >=
            this.box2.getLocationOnScreen().x &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().x <=
            this.box2.getLocationOnScreen().x + this.box2.width &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y >=
            this.box2.getLocationOnScreen().y &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y <=
            this.box2.getLocationOnScreen().y + this.box2.height
        ) {
          this.translateX = this.$refs[ref][0].nativeView.translateX;
          this.translateY = this.$refs[ref][0].nativeView.translateY;
          this.box2.scaleX = 1;
          this.box2.scaleY = 1;

          if (this.$refs[ref][0].nativeView.translateX <= -30) {
            this.$refs[ref][0].nativeView.translateX = -160;
          } else {
            this.$refs[ref][0].nativeView.translateX = 0;
          }
          if (this.$refs[ref][0].nativeView.translateY >= 115) {
            this.$refs[ref][0].nativeView.translateY = 140;
          } else {
            this.$refs[ref][0].nativeView.translateY = 0;
          }
          // Translate Animation Start 2
          // Handle Animation for swipe object from different position
          switch (ref) {
            case 0:
              if (
                this.$refs[this.boxArray.indexOf(this.boxArray[2])][0]
                  .nativeView.translateX >= 0
              ) {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[2])
                ][0].nativeView.translateX =
                  this.$refs[this.boxArray.indexOf(this.boxArray[2])][0]
                    .nativeView.translateX - 0;
              } else {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[2])
                ][0].nativeView.translateX =
                  this.$refs[this.boxArray.indexOf(this.boxArray[2])][0]
                    .nativeView.translateX + 0;
              }
              this.$refs[
                this.boxArray.indexOf(this.boxArray[2])
              ][0].nativeView.translateY =
                this.$refs[this.boxArray.indexOf(this.boxArray[2])][0]
                  .nativeView.translateY - 140;

              break;
            case 1:
              if (
                this.$refs[this.boxArray.indexOf(this.boxArray[2])][0]
                  .nativeView.translateX >= 0
              ) {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[2])
                ][0].nativeView.translateX =
                  160 -
                  this.$refs[this.boxArray.indexOf(this.boxArray[2])][0]
                    .nativeView.translateX;
              } else {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[2])
                ][0].nativeView.translateX =
                  160 +
                  this.$refs[this.boxArray.indexOf(this.boxArray[2])][0]
                    .nativeView.translateX;
              }
              this.$refs[
                this.boxArray.indexOf(this.boxArray[2])
              ][0].nativeView.translateY =
                this.$refs[this.boxArray.indexOf(this.boxArray[2])][0]
                  .nativeView.translateY - 140;
              break;
            case 3:
              if (
                this.$refs[this.boxArray.indexOf(this.boxArray[2])][0]
                  .nativeView.translateX >= 0
              ) {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[2])
                ][0].nativeView.translateX =
                  160 -
                  this.$refs[this.boxArray.indexOf(this.boxArray[2])][0]
                    .nativeView.translateX;
              } else {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[2])
                ][0].nativeView.translateX =
                  160 +
                  this.$refs[this.boxArray.indexOf(this.boxArray[2])][0]
                    .nativeView.translateX;
              }
              if (
                this.$refs[this.boxArray.indexOf(this.boxArray[2])][0]
                  .nativeView.translateY >= 0
              ) {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[2])
                ][0].nativeView.translateY =
                  0 +
                  this.$refs[this.boxArray.indexOf(this.boxArray[2])][0]
                    .nativeView.translateY;
              } else {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[2])
                ][0].nativeView.translateY =
                  0 -
                  this.$refs[this.boxArray.indexOf(this.boxArray[2])][0]
                    .nativeView.translateY;
              }
              break;
          }
          // Translate Animation End 2
          // Array that control Position drag item
          this.boxArray.splice(ref, 1, this.boxArray[2]);
          this.boxArray.splice(2, 1, box);
        } else if (
          // <========== BOX 3 ===========>
          this.$refs[ref][0].nativeView.getLocationOnScreen().x >=
            this.box3.getLocationOnScreen().x &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().x <=
            this.box3.getLocationOnScreen().x + this.box3.width &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y >=
            this.box3.getLocationOnScreen().y &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y <=
            this.box3.getLocationOnScreen().y + this.box3.height
        ) {
          this.translateX = this.$refs[ref][0].nativeView.translateX;
          this.translateY = this.$refs[ref][0].nativeView.translateY;
          this.box3.scaleX = 1;
          this.box3.scaleY = 1;
          if (this.$refs[ref][0].nativeView.translateX >= 120) {
            this.$refs[ref][0].nativeView.translateX = 160;
          } else {
            this.$refs[ref][0].nativeView.translateX = 0;
          }
          if (this.$refs[ref][0].nativeView.translateY >= 100) {
            this.$refs[ref][0].nativeView.translateY = 140;
          } else {
            this.$refs[ref][0].nativeView.translateY = 0;
          }
          // Translate Animation Start 3
          // Handle Animation for swipe object from different position
          switch (ref) {
            case 0:
              this.$refs[
                this.boxArray.indexOf(this.boxArray[3])
              ][0].nativeView.translateX =
                this.$refs[this.boxArray.indexOf(this.boxArray[3])][0]
                  .nativeView.translateX - 160;
              this.$refs[
                this.boxArray.indexOf(this.boxArray[3])
              ][0].nativeView.translateY =
                this.$refs[this.boxArray.indexOf(this.boxArray[3])][0]
                  .nativeView.translateY - 140;
              break;
            case 1:
              if (
                this.$refs[this.boxArray.indexOf(this.boxArray[3])][0]
                  .nativeView.translateX >= 0
              ) {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[3])
                ][0].nativeView.translateX =
                  this.$refs[this.boxArray.indexOf(this.boxArray[3])][0]
                    .nativeView.translateX - 0;
              } else {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[3])
                ][0].nativeView.translateX =
                  this.$refs[this.boxArray.indexOf(this.boxArray[3])][0]
                    .nativeView.translateX + 0;
              }
              this.$refs[
                this.boxArray.indexOf(this.boxArray[3])
              ][0].nativeView.translateY =
                this.$refs[this.boxArray.indexOf(this.boxArray[3])][0]
                  .nativeView.translateY - 140;
              break;
            case 2:
              this.$refs[
                this.boxArray.indexOf(this.boxArray[3])
              ][0].nativeView.translateX =
                this.$refs[this.boxArray.indexOf(this.boxArray[3])][0]
                  .nativeView.translateX - 160;
              if (
                this.$refs[this.boxArray.indexOf(this.boxArray[3])][0]
                  .nativeView.translateY >= 0
              ) {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[3])
                ][0].nativeView.translateY =
                  this.$refs[this.boxArray.indexOf(this.boxArray[3])][0]
                    .nativeView.translateY - 0;
              } else {
                this.$refs[
                  this.boxArray.indexOf(this.boxArray[3])
                ][0].nativeView.translateY =
                  this.$refs[this.boxArray.indexOf(this.boxArray[3])][0]
                    .nativeView.translateY + 0;
              }
              break;
          }
          // Translate Animation End 3
          // Array that control Position drag item
          this.boxArray.splice(ref, 1, this.boxArray[3]);
          this.boxArray.splice(3, 1, box);
        } else {
          setTimeout(() => {
            this.$refs[ref][0].nativeView.translateX = this.translateX;
            this.$refs[ref][0].nativeView.translateY = this.translateY;
          }, 100);
        }
      }
    },
  },
};
</script>

<style lang="scss" scoped>
// @import "./booking.scss";
.box {
  margin: 15;
  width: 130;
  height: 110;
}

.solid {
  width: 90;
  height: 70;
}

.timer {
  height: 80;
  width: 80;
  border-radius: 50%;
  background: #ffffff;
}

.pie {
  border-radius: 50%;
  background: linear-gradient(270deg, transparent 50%, #0d9dff 50%);
}

.fill {
  border-radius: 50%;
}
</style>
