<template>
  <button @click="openModal" class="btn btn-primary edit-btn" v-if="!showModal" >Clip Video</button>
<!--  Modal to appear only when showModal is set to true -->
<div id="Chanl-video" :class="{ 'show': showModal }" v-if="showModal" >
<!-- Button to open the modal -->

<!-- Modal content -->
  <div class="modal" tabindex="-1" role="dialog" >
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="card-title">
<!--          Binding title property-->
          <span v-if="!isTitleEditable">{{ title }}</span>
          <input v-else v-model="title" @blur="saveTitle" />
          <button @click="toggleTitleEditing" class="btn btn-link edit-btn">
            {{ isTitleEditable ? 'Save' : 'Edit' }}
          </button>
        </h5>
        <button type="btn btn-primary" class="close close-btn" @click="closeModal">
          <span aria-hidden="true">Close Modal</span>
        </button>
      </div>
      <div class="modal-body">
        <!-- Video player -->
        <video  v-if="showModal"  ref="videoPlayer" controls @timeupdate="updateTimeRange">
          <source :src="videoSrc" type="video/mp4">
        </video>
      </div>
      <div class="modal-footer">
        <label for="start-time">From:</label>
        <input id="start-time" type="text" v-model="startTime" @input="updateVideoTime">

        <label for="end-time">To:</label>
        <input id="end-time" type="text" v-model="endTime" @input="updateVideoTime">

<!--        Button to download the video-->
        <a :href="videoSrc" download class="btn btn-secondary">Download</a>
        <!-- Button to emit params to params component  -->
        <button @click="downloadClip" class="btn btn-primary">Clip</button>
        <!-- Button to play/pause the video -->
        <button @click="playVideo" class="btn btn-primary">{{ isPlaying ? 'Pause Chanl Video' : 'Play Chanl Video' }}</button>
      </div>
    </div>
  </div>
</div>
</div>
</template>
<script>
export default {
  name: "ChanlVideo",
  data() {
    return {
      showModal: false,
      videoSrc: 'https://cdn.plyr.io/static/demo/View_From_A_Blue_Moon_Trailer-1080p.mp4',
      startTime: '0:00',
      endTime: '0:00',
      title:'',
      isPlaying: false,
      isTitleEditable: false,
    };

  },
  methods: {
    openModal() {
      this.showModal = true;
      this.$nextTick(() => {
        if (this.$refs.videoPlayer) {
          this.$refs.videoPlayer.currentTime = 0;
          this.$refs.videoPlayer.play();
        }
      });
    },
    closeModal() {
      if (this.$refs.videoPlayer) {
        this.$refs.videoPlayer.pause();
      }
      this.showModal = false;
    },

    //edit the title here
    toggleTitleEditing() {
      this.isTitleEditable = !this.isTitleEditable;
    },
    saveTitle() {
      this.isTitleEditable = false;
    },


    updateTimeRange() {
      if (this.$refs.videoPlayer) {
        const currentTime = this.$refs.videoPlayer.currentTime;
        const duration = this.$refs.videoPlayer.duration;
        this.startTime = this.formatTime(currentTime);
        this.endTime = this.formatTime(duration);
      }
    },

    formatTime(time) {
      const minutes = Math.floor(time / 60);
      const seconds = Math.floor(time % 60).toFixed(2);
      return `${minutes}:${seconds.padStart(5, '0')}`;
    },

    //toggle the play so that you can either play or pause
    playVideo() {
      if (this.isPlaying) {
        this.$refs.videoPlayer.pause();
        this.isPlaying = false;
      } else {
        this.$refs.videoPlayer.play();
        this.isPlaying = true;
      }
    },
    //toggle the play input so that you can update it directly
    updateVideoTime() {
      const startParts = this.startTime.split(':');
      const endParts = this.endTime.split(':');
      const startMinutes = parseInt(startParts[0]);
      const startSeconds = parseFloat(startParts[1]);
      const endMinutes = parseInt(endParts[0]);
      const endSeconds = parseFloat(endParts[1]);
      const startInSeconds = startMinutes * 60 + startSeconds;
      const endInSeconds = endMinutes * 60 + endSeconds;

      if (this.$refs.videoPlayer) {
        this.$refs.videoPlayer.currentTime = startInSeconds;
        this.$refs.videoPlayer.play();
        this.isPlaying = true;

        if (endInSeconds > startInSeconds) {
          this.$refs.videoPlayer.addEventListener('timeupdate', () => {
            if (this.$refs.videoPlayer && this.$refs.videoPlayer.currentTime >= endInSeconds) {
              this.$refs.videoPlayer.pause();
              this.isPlaying = false;
            }
          });
        }
      }
    },


    // Emit the clip parameters to the parent component
    downloadClip() {
      const clipParams = {
        download: 'download clip',
        start: this.startTime,
        end: this.endTime,
        title:this.title,
      };
      this.$emit('clip-submitted', clipParams);
    }
  }
};
</script>

<!--bootstrap css-->
<style scoped>
#Chanl-video {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;

  margin: 2rem;
  border-radius: 14px;
  max-width: 400px;
  border: 5px solid #ddd;
  display: flex;
  padding: 2rem;
  padding-top: 20px;
  justify-content: space-between;
  border-bottom: 5px solid #ddd;
}

.clip-video {
  display: flex;
  padding: 1rem;
  justify-content: space-between;
  border-bottom: 1px solid #ddd;
}

.modal {
  font-size: 0.875rem;
  background: #eee;
  margin: 0 0 0 0.5rem;
  height: auto;
  border-radius: 5px;
  transition: all 0.1s ease-out;
  color: rgba(0, 0, 0, 0.5);
  cursor: pointer;
  padding: 1rem;
}

.modal-body video {
  max-width: 100%;
}

.modal-footer {
  margin-top: 1rem;
}
.edit-btn{
  margin-top: 1rem;
  font-size: 0.875rem;
  background: #eee;
  border-radius: 14px;
  max-width: 100px;
  border: 2px solid #ddd;
  display: flex;
  padding: 1rem;
  order: 1;
}
.close-btn{
  order: 2;
  font-size: 0.875rem;
  background: red;
  border-radius: 14px;
  max-width: 300px;
  border: 2px solid #ddd;
  display: flex;
  padding: 1rem;
  /*padding-left: 5px;*/
  margin-top: -4rem;
  margin-left: auto;
}
.modal-footer label {
  margin-right: 0.5rem;
}

.modal-footer input[type="number"] {
  margin-right: 1rem;
}

.modal-footer button {
  margin-top: 0.5rem;
}

.card-text .buttons {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.edit-btn {
  order: 1;
}

.close-btn {
  order: 2;
}


.modal-footer:hover {
  background: #ddd;
  color: black;
}

p {
  color: rgba(0,0,0,0.6);
  line-height: 2rem;
}
</style>