<template>
  <!-- Main content -->
  <section class="content">
    <!-- GitHub hint -->
<!--    <div class="row">-->
<!--      <div class="col-xs-12">-->
<!--        <alert :dismissible="true"-->
<!--               type="success"-->
<!--               :iconClasses="['fa', 'fa-check']"-->
<!--               title="CoPilot is open source!">-->
<!--          <span>Click on icon to check it out on github.</span>-->
<!--          <a href="https://github.com/misterGF/CoPilot" target="_blank">-->
<!--            <i class="fa fa-github fa-2x"></i>-->
<!--          </a>-->
<!--        </alert>-->
<!--      </div>-->

      <!-- Info boxes -->
      <div class="col-md-3 col-sm-6 col-xs-12">
        <info-box color-class="bg-orange"
                  :icon-classes="['fa', 'fa-facebook-official']"
                  text="Bài đăng trên MXH"
                  number="6888"></info-box>
      </div>
      <!-- /.col -->
      <div class="col-md-3 col-sm-6 col-xs-12">
        <info-box color-class="bg-green"
                  :icon-classes="['ion', 'ion-ios-chatbubble-outline']"
                  text="Bình luận trên MXH"
                  number="8888666"></info-box>
      </div>
      <!-- /.col -->

      <!-- fix for small devices only -->
      <div class="clearfix visible-sm-block"></div>

      <div class="col-md-3 col-sm-6 col-xs-12">
        <info-box color-class="bg-red"
                  :icon-classes="['fa', 'fa-newspaper-o']"
                  text="Báo chí, Tin tức"
                  number="760"></info-box>
      </div>
      <!-- /.col -->
      <div class="col-md-3 col-sm-6 col-xs-12">
        <info-box color-class="bg-aqua"
                  :icon-classes="['ion', 'ion-ios-people-outline']"
                  text="Nguồn khác(Diễn đàn, website...)"
                  number="1000"></info-box>
      </div>
      <!-- /.col -->
<!--    </div>-->
    <!-- /.row -->

    <div class="col-xs-12">
      <div class="box">
        <div class="box-header with-border">
          <h3 class="box-title"></h3>
          <div class="box-body">
            <div class="col-sm-6 col-xs-12">
              <p class="text-center">
                <strong>Số lượng nội dung có đề cập</strong>
              </p>
              <canvas id="trafficBar" ></canvas>
            </div>
            <hr class="visible-xs-block">
            <div class="col-sm-6 col-xs-12">
              <p class="text-center">
                <strong>Tổng quan sắc thái</strong>
              </p>
              <canvas id="classification"></canvas>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- /.row -->

    <!-- Main row -->
    <div class="row">
      <div class="col-md-3 col-sm-6 col-xs-12">
        <process-info-box color-class="bg-yellow"
                          :icon-classes="['fa', 'fa-facebook-official']"
                          text="Số bài đăng nhắc tới từ khóa trên MXH"
                          number="5,200/6888"
                          :progress="50"
                          description="50% Trong tổng số bài đăng"></process-info-box>
      </div>
      <!-- /.col -->
      <div class="col-md-3 col-sm-6 col-xs-12">
        <process-info-box color-class="bg-green"
                          :icon-classes="['ion', 'ion-ios-chatbubble-outline']"
                          text="Số bình luận MXH nhắc đến từ khóa"
                          number="92,050/8888666"
                          :progress="20"
                          description="20% increase in 30 days"></process-info-box>
      </div>
      <!-- /.col -->
      <div class="col-md-3 col-sm-6 col-xs-12">
        <process-info-box color-class="bg-red"
                          :icon-classes="['fa', 'fa-newspaper-o']"
                          text="Số bài báo , tin tức nhắc đến từ kho"
                          number="530/760"
                          :progress="70"
                          description="70% Tổng số bài báo, tin tức"></process-info-box>
      </div>
      <!-- /.col -->
      <div class="col-md-3 col-sm-6 col-xs-12">
        <process-info-box color-class="bg-aqua"
                          :icon-classes="['ion', 'ion-ios-people-outline']"
                          text="Số nội dung nhắc tới từ khóa trên diễn đàn, blog & website"
                          number="400/1000"
                          :progress="40"
                          description="40% increase compared to last year"></process-info-box>
      </div>
      <!-- /.col -->
    </div>
    <!-- /.row -->
  </section>
  <!-- /.content -->
</template>

<script>
import Chart from 'chart.js'
import Alert from '../widgets/Alert'
import InfoBox from '../widgets/InfoBox'
import ProcessInfoBox from '../widgets/ProcessInfoBox'

export default {
  name: 'Dashboard',
  components: {
    Alert,
    InfoBox,
    ProcessInfoBox
  },
  data () {
    return {
      generateRandomNumbers (numbers, max, min) {
        var a = []
        for (var i = 0; i < numbers; i++) {
          a.push(Math.floor(Math.random() * (max - min + 1)) + max)
        }
        return a
      }
    }
  },
  computed: {
    numberMXH () {
      return this.generateRandomNumbers(12, 1000000, 10000)
    },
    numberComments () {
      return this.generateRandomNumbers(12, 80000, 10000)
    },
    numberNewspaper () {
      return this.generateRandomNumbers(12, 650000, 10000)
    },
    numberDifferent () {
      return this.generateRandomNumbers(12, 4788888, 10000)
    },
    isMobile () {
      return (window.innerWidth <= 800 && window.innerHeight <= 600)
    }
  },
  mounted () {
    this.$nextTick(() => {
      var ctx = document.getElementById('trafficBar').getContext('2d')
      var config = {
        type: 'line',
        data: {
          labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'],
          datasets: [{
            label: 'Bài đăng MXH',
            fill: false,
            borderColor: 'orange',
            pointBackgroundColor: 'orange',
            backgroundColor: 'rgba(0, 0, 0, 0)',
            data: this.numberMXH
          }, {
            label: 'Bình luận MXH',
            borderColor: 'green',
            pointBackgroundColor: 'green',
            backgroundColor: 'rgba(0, 0, 0, 0)',
            data: this.numberComments
          }, {
            label: 'Báo chí, Tin tức',
            borderColor: 'red',
            pointBackgroundColor: 'red',
            backgroundColor: 'rgba(0, 0, 0, 0)',
            data: this.numberNewspaper
          }, {
            label: 'Nguồn khác(diễn đàn, blog & website)',
            borderColor: 'aqua',
            pointBackgroundColor: 'aqua',
            backgroundColor: 'rgba(0, 0, 0, 0)',
            data: this.numberDifferent
          }]
        },
        options: {
          responsive: true,
          maintainAspectRatio: !this.isMobile,
          legend: {
            position: 'bottom',
            display: true
          },
          tooltips: {
            mode: 'label',
            xPadding: 10,
            yPadding: 10,
            bodySpacing: 10
          }
        }
      }

      new Chart(ctx, config) // eslint-disable-line no-new

      var pieChartCanvas = document.getElementById('classification').getContext('2d')
      var pieConfig = {
        type: 'pie',
        data: {
          labels: ['Tích cực', 'Tiêu cực', 'Trung tính'],
          datasets: [{
            data: [40, 38, 22],
            backgroundColor: ['#00a65a', '#f39c12', '#00c0ef'],
            hoverBackgroundColor: ['#00a65a', '#f39c12', '#00c0ef']
          }]
        },
        options: {
          responsive: true,
          maintainAspectRatio: !this.isMobile,
          legend: {
            position: 'bottom',
            display: true
          }
        }
      }

      new Chart(pieChartCanvas, pieConfig) // eslint-disable-line no-new
    })
  }
}
</script>
<style>
.info-box {
  cursor: pointer;
}
.info-box-content {
  text-align: center;
  vertical-align: middle;
  display: inherit;
}
.fullCanvas {
  width: 100%;
}
</style>
