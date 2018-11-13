<template>

    <div class="card_A">

        <!-- wwManager:start -->
        <wwSectionEditMenu v-bind:section="section"></wwSectionEditMenu>
        <!-- wwManager:end -->

        <wwObject class="background" v-bind:ww-object="section.data.background" ww-category="background"></wwObject>

        <!--TOP WWOBJS-->
        <div class="top-ww-objs">
            <div class="top-ww-obj" v-for="topWwObj in section.data.topWwObjs" :key="topWwObj.uniqueId">
                <wwObject v-bind:ww-object="topWwObj"></wwObject>
            </div>
        </div>

        <!--CARD-->
        <div class="card">
            <wwObject class="background" v-bind:ww-object="section.data.cardBackground" ww-category="background"></wwObject>
            <div class="card-content">
                <!-- COL 1 -->
                <div class="col">
                    <div class="content" v-for="content in section.data.col1" :key="content.uniqueId">
                        <wwObject v-bind:ww-object="content"></wwObject>
                    </div>
                </div>
                <!-- COL 2 -->
                <div class="col">
                    <div class="content" v-for="content in section.data.col2" :key="content.uniqueId">
                        <wwObject v-bind:ww-object="content"></wwObject>
                    </div>
                </div>
            </div>
        </div>

        <!--BOTTOM WWOBJS-->
        <div class="bottom-ww-objs">
            <div class="top-ww-obj" v-for="bottomWwObj in section.data.bottomWwObjs" :key="bottomWwObj.uniqueId">
                <wwObject v-bind:ww-object="bottomWwObj"></wwObject>
            </div>
        </div>

    </div>
</template>


<script>
export default {
    name: "card_A",
    props: {
        sectionCtrl: Object
    },
    data() {
        return {
            section: this.sectionCtrl.get()
        }
    },
    computed: {
    },
    methods: {
        init: function (section) {
            this.section.data.topWwObjs = this.section.data.topWwObjs || [];
            this.section.data.bottomWwObjs = this.section.data.bottomWwObjs || [];
            this.section.data.col1 = this.section.data.col1 || [];
            this.section.data.col2 = this.section.data.col2 || [];
        }
    },
    created: function () { },
    mounted: function () {
        this.init()
    }
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
