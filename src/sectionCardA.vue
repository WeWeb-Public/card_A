<template>

    <div class="card_A">

        <!-- wwManager:start -->
        <wwSectionEditMenu v-bind:sectionCtrl="sectionCtrl"></wwSectionEditMenu>
        <!-- wwManager:end -->

        <wwObject class="background" v-bind:ww-object="section.data.background" ww-category="background"></wwObject>

        <!--TOP WWOBJS-->
        <div class="top-ww-objs">
            <wwLayoutColumn tag='div' ww-default="ww-image" :ww-list="section.data.topWwObjs" class="top-ww-obj" @ww-add="add(section.data.topWwObjs, $event)" @ww-remove="remove(section.data.topWwObjs, $event)">
                <wwObject v-for="topWwObj in section.data.topWwObjs" :key="topWwObj.uniqueId" v-bind:ww-object="topWwObj"></wwObject>
            </wwLayoutColumn>
        </div>

        <!--CARD-->
        <div class="card">
            <wwObject class="background" v-bind:ww-object="section.data.cardBackground" ww-category="background"></wwObject>
            <div class="card-content">
                <!-- COL 1 -->
                <div class="col">
                    <wwLayoutColumn tag='div' ww-default="ww-image" :ww-list="section.data.col1" class="content" @ww-add="add(section.data.col1, $event)" @ww-remove="remove(section.data.col1, $event)">
                        <wwObject v-for="content in section.data.col1" :key="content.uniqueId" v-bind:ww-object="content"></wwObject>
                    </wwLayoutColumn>
                </div>
                <!-- COL 2 -->
                <div class="col">
                    <wwLayoutColumn tag='div' ww-default="ww-image" :ww-list="section.data.col2" class="content" @ww-add="add(section.data.col2, $event)" @ww-remove="remove(section.data.col2, $event)">
                        <wwObject v-for="content in section.data.col2" :key="content.uniqueId" v-bind:ww-object="content"></wwObject>
                    </wwLayoutColumn>
                </div>
            </div>
        </div>

        <!--BOTTOM WWOBJS-->
        <div class="bottom-ww-objs">
            <wwLayoutColumn tag='div' ww-default="ww-image" :ww-list="section.data.bottomWwObjs" class="top-ww-obj" @ww-add="add(section.data.bottomWwObjs, $event)" @ww-remove="remove(section.data.bottomWwObjs, $event)">
                <wwObject v-for="bottomWwObj in section.data.bottomWwObjs" :key="bottomWwObj.uniqueId" v-bind:ww-object="bottomWwObj"></wwObject>
            </wwLayoutColumn>
        </div>

    </div>
</template>


<script>
export default {
    name: "__COMPONENT_NAME__",
    props: {
        sectionCtrl: Object
    },
    data() {
        return {
        }
    },
    computed: {
        section() {
            return this.sectionCtrl.get();
        }
    },
    methods: {
        initData() {
            //Init objects
            let needUpdate = false;
            if (!this.section.data.background) {
                this.section.data.background = wwLib.wwObject.getDefault({ type: 'ww-color', data: { color: 'white' } });
                needUpdate = true;
            }
            if (!this.section.data.cardBackground) {
                this.section.data.cardBackground = wwLib.wwObject.getDefault({ type: 'ww-color', data: { color: 'white' } });
                needUpdate = true;
            }
            if (_.isEmpty(this.section.data.topWwObjs)) {
                this.section.data.topWwObjs = [];
                needUpdate = true;
            }
            if (_.isEmpty(this.section.data.bottomWwObjs)) {
                this.section.data.bottomWwObjs = [];
                needUpdate = true;
            }
            if (_.isEmpty(this.section.data.col1)) {
                this.section.data.col1 = [];
                needUpdate = true;
            }
            if (_.isEmpty(this.section.data.col2)) {
                this.section.data.col2 = [];
                needUpdate = true;
            }
            if (needUpdate) {
                this.sectionCtrl.update(this.section);
            }
        },
        add(list, options) {
            list.splice(options.index, 0, options.wwObject);

            this.sectionCtrl.update(this.section);
        },
        remove(list, options) {
            list.splice(options.index, 1);

            this.sectionCtrl.update(this.section);
        }
    },
    created: function () {
        this.initData();
    },
    mounted: function () { }
};
</script>

<style scoped>
.card_A {
  position: relative;
}

.background {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
}

.top-ww-objs,
.bottom-ww-objs {
  position: relative;
}

.card {
  margin: 20px 8.333333%;
  position: relative;
  min-height: 200px;
  box-shadow: 0 2px 80px 0 rgba(209, 209, 209, 0.5);
}

.card-content {
  position: relative;
  display: flex;
  align-items: center;
  flex-wrap: wrap;
}

.col {
  position: relative;
  padding: 0;
  flex-basis: 100%;
}

@media (min-width: 769px) {
  .col {
    flex-basis: 50%;
  }
}
</style>
