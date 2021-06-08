<template>
  <li
    class="song-item"
    @click="
      $emit('update:music', { item, index });
      $emit('update:playlist');
    "
  >
    <div class="info">
      <h5>{{ item.name }}</h5>
      <p>
		<i class="sghot"></i>
        <span class="three" v-for="(artist, index) in item.song.artists" :key="index">
          <template v-if="index"> / </template>{{ artist.name }}
        </span>
		<span class="three">{{item.name}}</span>
      </p>
    </div>
    <div class="icon">
      <span
        class="playing"
        :class="{ paused: paused }"
        v-if="currentMusic && currentMusic.id === item.id"
      >
        <i></i>
        <i></i>
        <i></i>
      </span>
      <span class="Playicon" v-else>▶</span>
    </div>
  </li>
</template>

<script>
export default {
  props: ["item", "index", "currentMusic", "paused"],
  // created() {
  //   console.log('$root',this.$root);
  //   console.log('$parent',this.$parent);
  // },
};
</script>

<style lang="less">
li.song-item {
  display: flex;
  line-height: 23px;
  padding: 8px 10px 0 10px;
  .info {
    flex: 1;
	.three{
		font-size: 12px;
		color: #888;
	}
	.sghot{
		display: inline-block;
		width: 12px;
		height: 8px;
		margin-right: 4px;
		margin-bottom: 2px;
		background: url(https://s3.music.126.net/mobile-new/img/index_icon_2x.png?5207a28c3767992ca4bb6d4887c74880=) no-repeat;
		background-size: 166px 97px;
		font-size: 12px;
		color: #888;
	}
  }
  .icon {
    width: 30px;
    height: 30px;
	.Playicon{
		display: inline-block;
		width: 25px;
		height: 25px;
		padding-left: 7px;
		line-height: 22px;
		border-radius: 50%;
		border: 1px solid #ccc;
		color: #ccc;
		font-size: 14px;
	}
    .playing {
      display: flex;
      justify-content: space-between;
      align-items: flex-end;
      i {
        width: 6px;
        height: 30px;
        background: red;
        // display: inline-block;
        transform-origin: center bottom;

        animation: playing 0.6s linear -0.2s infinite alternate-reverse;

        &:first-of-type {
          animation-delay: 0s;
        }
        &:last-of-type {
          animation-delay: -0.4s;
        }
      }
      &.paused {
        i {
          animation-play-state: paused;
        }
      }
    }
  }
}

@keyframes playing {
  from {
    // height: 50px;
    transform: scaleY(1);
  }
  to {
    // height: 10px;
    transform: scaleY(0.2);
  }
}
</style>