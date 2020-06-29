<template>
  <div>
    <input type="text" v-stream:input="input$">
    {{ message$ }}
  </div>
</template>

<script>
import { pluck, scan } from 'rxjs/operators'

let subscriptions = function() {
  let message$ = this.input$.pipe(
    pluck('event', 'data'),
    scan((a, x) => a + x)
  )

  return { message$ }
}

export default {
  name: 'app',
  domStreams: [
    'input$'
  ],
  subscriptions
}
</script>
