<template>
  <b-collapse class="card" animation="slide" aria-id="contentIdForA11y3" :open=false>
            <div
                slot="trigger" 
                slot-scope="props"
                class="card-header"
                role="button"
                
                aria-controls="contentIdForA11y3">
                <p class="card-header-title">
                    {{ title }} : {{ formatTotalTime }}　
                  <b-taglist>
                    <b-tag type="is-primary is-light">確認待ち</b-tag>
                  </b-taglist>
                </p>
                <a class="card-header-icon">
                    <b-icon
                        :icon="props.open ? 'menu-up' : 'menu-down'">
                    </b-icon>
                </a>
            </div>
            <div class="card-content">
                <div class="content">
                    ほにゃらら
                </div>
            </div>
            <footer class="card-footer">
            <slot />

            </footer>
        </b-collapse>
        
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      required: true
    },
    formatsec: {},
    totalsec: {},
  },
  computed: {
    formatTime: function() {
      var sec = this.formatsec
      return this.SecToTime(sec)
    },
    formatTotalTime: function(){
      var rawsec = this.totalsec
      return this.SecToTime(rawsec)
    }
  },


}
</script>
