<template>
  <div id="about">
    <div class="container">
      <div class="row">
        <div class="col-md-6">
          <h1>Video instructions</h1>
          <p>Home is the parent Component .</p>
          <p>The ChanlVideo Component is the child containing the functionalities of the clip and params that will be emitted to parent </p>
          <p>I have used a default video shared with me for testing</p>
          <p>I have used bootstrap for styling </p>
          <p>When Download button to video source and when clicked, it triggers the download of the video</p>
          <p>The start time (From) and end time (To) can be updated directly by entering the input</p>
          <p>Clip button below the video is for emitting params to parent compoents.Such params are title,endtime,start time </p>
          <p>play Chanl Video button is used to toggle between playing and pausing the video button below the video </p>
        </div>
        <div class="col-md-6">
          <h1>Code Explanation</h1>
          <p>The $nexttick is for ensuring that the video player is properly initialized and the video starts playing.</p>
          <p>From and to inputs displays the current time range of the video .The UpdateTimeRange method is called during the video's (Timeupdate) event which is triggered when video is playing</p>
          <p>The formatTime method is for formatting time in the mm:ss.sss format</p>
          <p>The "Play Chanl Video " button will toggle between playing and pausing the video based on the isPlaying flag. Initially, isPlaying is set to false. When the button is clicked, it will either play or pause the video accordingly and update the isPlaying flag.</p>
          <p>The @input event listener in the start and end time inputs elements. When the input values are changed, the updateVideoTime method is called, which updates the video player's current time based on the entered start and end times.</p>
          <p>Additionally, the updateVideoTime method also handles playing and pausing the video based on the entered time range.</p>
          <p>To make the title editable,  I  have  used an input field and bind it to a data property.I have just used a placeholder but can be editable</p>
          <p>The Title is updated when the video is clipped and params displayed in parent Component</p>
          <p>updateVideoTime() method:
            This method is responsible for updating the video player's current time and playing the video based on the selected time range.
          </p>
          <p>updateTimeRange()
            This method is responsible for updating the time range of the video based on the current time of the video player.
            It retrieves the current time of the video player using this.$refs.videoPlayer.currentTime.
            It also retrieves the total duration of the video using this.$refs.videoPlayer.duration.</p>
          <p>The video player is then played using this.$refs.videoPlayer.play(), and the isPlaying flag is set to true to indicate that the video is playing.</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
#about {
  max-width: 650px;
}

p {
  color: rgba(0, 0, 0, 0.6);
  line-height: 2rem;
}
</style>
