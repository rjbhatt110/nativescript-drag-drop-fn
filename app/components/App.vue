<template>
  <Page>
    <ActionBar title="Drag and Drop Nativescript" />
    <StackLayout>
      <GridLayout
        ref="grid"
        rows="auto, auto"
        columns="auto,auto"
        verticalAlignment="top"
        horizontalAlignment="center"
      >
        <Image
          ref="dropArea0"
          src="res://droparea"
          row="0"
          col="0"
          class="droparea_square"
        />
        <Image
          ref="dropArea1"
          src="res://droparea"
          row="0"
          col="1"
          class="droparea_square"
        />
        <Image
          ref="dropArea2"
          src="res://droparea"
          row="1"
          col="0"
          class="droparea_square"
        />
        <Image
          ref="dropArea3"
          src="res://droparea"
          row="1"
          col="1"
          class="droparea_square"
        />
        <Image
          v-for="(drag, index) in boxArray"
          :key="drag.refId"
          :ref="index"
          :src="drag.src"
          :row="drag.row"
          :col="drag.col"
          class="drag_item"
          @pan="onPan($event, index, drag)"
        />
      </GridLayout>
      <Image src="res://correct" width="50" height="50" v-if="right" />
    </StackLayout>
  </Page>
</template>

<script>
import { PanGestureEventData } from "ui/gestures";

export default {
  name: "Home",
  data() {
    return {
      right: false,
      boxArray: [
        {
          refId: "drag4",
          row: 0,
          col: 0,
          src: "res://dragbox4",
        },
        {
          refId: "drag1",
          row: 0,
          col: 1,
          src: "res://dragbox1",
        },
        {
          refId: "drag2",
          row: 1,
          col: 0,
          src: "res://dragbox2",
        },
        {
          refId: "drag3",
          row: 1,
          col: 1,
          src: "res://dragbox3",
        },
      ],
      finalArray: [
        {
          refId: "drag1",
          row: 0,
          col: 1,
          src: "res://dragbox1",
        },
        {
          refId: "drag2",
          row: 1,
          col: 0,
          src: "res://dragbox2",
        },
        {
          refId: "drag3",
          row: 1,
          col: 1,
          src: "res://dragbox3",
        },
        {
          refId: "drag4",
          row: 0,
          col: 0,
          src: "res://dragbox4",
        },
      ],
    };
  },
  computed: {},
  created() {},
  mounted() {
    this.dropArea0 = this.$refs.dropArea0.nativeView;
    this.dropArea1 = this.$refs.dropArea1.nativeView;
    this.dropArea2 = this.$refs.dropArea2.nativeView;
    this.dropArea3 = this.$refs.dropArea3.nativeView;
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
            this.dropArea0.getLocationOnScreen().x &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().x <=
            this.dropArea0.getLocationOnScreen().x + this.dropArea0.width &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y >=
            this.dropArea0.getLocationOnScreen().y &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y <=
            this.dropArea0.getLocationOnScreen().y + this.dropArea0.height
        ) {
          this.dropArea0.scaleX = 1.1;
          this.dropArea0.scaleY = 1.1;
        } else {
          this.dropArea0.scaleX = 1;
          this.dropArea0.scaleY = 1;
        }

        if (
          this.$refs[ref][0].nativeView.getLocationOnScreen().x >=
            this.dropArea1.getLocationOnScreen().x &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().x <=
            this.dropArea1.getLocationOnScreen().x + this.dropArea1.width &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y >=
            this.dropArea1.getLocationOnScreen().y &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y <=
            this.dropArea1.getLocationOnScreen().y + this.dropArea1.height
        ) {
          this.dropArea1.scaleX = 1.1;
          this.dropArea1.scaleY = 1.1;
        } else {
          this.dropArea1.scaleX = 1;
          this.dropArea1.scaleY = 1;
        }

        if (
          this.$refs[ref][0].nativeView.getLocationOnScreen().x >=
            this.dropArea2.getLocationOnScreen().x &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().x <=
            this.dropArea2.getLocationOnScreen().x + this.dropArea2.width &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y >=
            this.dropArea2.getLocationOnScreen().y &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y <=
            this.dropArea2.getLocationOnScreen().y + this.dropArea2.height
        ) {
          this.dropArea2.scaleX = 1.1;
          this.dropArea2.scaleY = 1.1;
        } else {
          this.dropArea2.scaleX = 1;
          this.dropArea2.scaleY = 1;
        }

        if (
          this.$refs[ref][0].nativeView.getLocationOnScreen().x >=
            this.dropArea3.getLocationOnScreen().x &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().x <=
            this.dropArea3.getLocationOnScreen().x + this.dropArea3.width &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y >=
            this.dropArea3.getLocationOnScreen().y &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y <=
            this.dropArea3.getLocationOnScreen().y + this.dropArea3.height
        ) {
          this.dropArea3.scaleX = 1.1;
          this.dropArea3.scaleY = 1.1;
        } else {
          this.dropArea3.scaleX = 1;
          this.dropArea3.scaleY = 1;
        }
        // UP
      } else if (args.state === 3) {
        if (
          // <========== Drop Area 0 ===========>
          this.$refs[ref][0].nativeView.getLocationOnScreen().x >=
            this.dropArea0.getLocationOnScreen().x &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().x <=
            this.dropArea0.getLocationOnScreen().x + this.dropArea0.width &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y >=
            this.dropArea0.getLocationOnScreen().y &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y <=
            this.dropArea0.getLocationOnScreen().y + this.dropArea0.height
        ) {
          this.translateX = this.$refs[ref][0].nativeView.translateX;
          this.translateY = this.$refs[ref][0].nativeView.translateY;
          this.dropArea0.scaleX = 1;
          this.dropArea0.scaleY = 1;

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
          // <========== Drop Area 1 ===========>
          this.$refs[ref][0].nativeView.getLocationOnScreen().x >=
            this.dropArea1.getLocationOnScreen().x &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().x <=
            this.dropArea1.getLocationOnScreen().x + this.dropArea1.width &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y >=
            this.dropArea1.getLocationOnScreen().y &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y <=
            this.dropArea1.getLocationOnScreen().y + this.dropArea1.height
        ) {
          this.translateX = this.$refs[ref][0].nativeView.translateX;
          this.translateY = this.$refs[ref][0].nativeView.translateY;
          this.dropArea1.scaleX = 1;
          this.dropArea1.scaleY = 1;
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
          // <========== Drop Area 2 ===========>
          this.$refs[ref][0].nativeView.getLocationOnScreen().x >=
            this.dropArea2.getLocationOnScreen().x &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().x <=
            this.dropArea2.getLocationOnScreen().x + this.dropArea2.width &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y >=
            this.dropArea2.getLocationOnScreen().y &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y <=
            this.dropArea2.getLocationOnScreen().y + this.dropArea2.height
        ) {
          this.translateX = this.$refs[ref][0].nativeView.translateX;
          this.translateY = this.$refs[ref][0].nativeView.translateY;
          this.dropArea2.scaleX = 1;
          this.dropArea2.scaleY = 1;

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
          // <========== Drop Area 3 ===========>
          this.$refs[ref][0].nativeView.getLocationOnScreen().x >=
            this.dropArea3.getLocationOnScreen().x &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().x <=
            this.dropArea3.getLocationOnScreen().x + this.dropArea3.width &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y >=
            this.dropArea3.getLocationOnScreen().y &&
          this.$refs[ref][0].nativeView.getLocationOnScreen().y <=
            this.dropArea3.getLocationOnScreen().y + this.dropArea3.height
        ) {
          this.translateX = this.$refs[ref][0].nativeView.translateX;
          this.translateY = this.$refs[ref][0].nativeView.translateY;
          this.dropArea3.scaleX = 1;
          this.dropArea3.scaleY = 1;
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
        if (JSON.stringify(this.boxArray) === JSON.stringify(this.finalArray)) {
          this.right = true;
        }
      }
    },
  },
};
</script>

<style lang="scss" scoped>
// @import "./booking.scss";
.droparea_square {
  margin: 15;
  width: 130;
  height: 110;
}

.drag_item {
  width: 90;
  height: 70;
}
</style>
