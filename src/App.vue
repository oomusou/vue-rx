<template>
  <div>
    <button v-stream:click="click$">Show Message</button>
    <div>{{ message$ }}</div>
  </div>
</template>

<script>
import { concat, EMPTY } from 'rxjs'
import { startWith, delay, switchMapTo } from 'rxjs/operators'

let delayMsg$ = x => EMPTY.pipe(
  startWith(x),
  delay(1000)
)

let subscriptions = function() {
  let slogan$ = concat(
    delayMsg$('Get Ready!'),
    delayMsg$(3),
    delayMsg$(2),
    delayMsg$(1),
    delayMsg$('Go!')
  )

  let message$ = this.click$.pipe(
    switchMapTo(slogan$)
  )

  return { message$ }
}

export default {
  name:'App',
  domStreams: [
    'click$'
  ],
  subscriptions
}
</script>

