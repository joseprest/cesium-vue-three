<template>
  <div>
    <div id="player"></div>
    <div id="overlay" class="overlay">
      <div>
        <div id="qualityStatus" class="greyStatus"></div>
        <div id="overlayButton">+</div>
      </div>
      <div id="overlaySettings">
        <div id="KickOthers">
          <div class="settings-text">Kick all other players</div>
          <label class="btn-overlay">
            <input
              type="button"
              id="kick-other-players-button"
              class="overlay-button btn-flat"
              value="Kick"
            />
          </label>
        </div>
        <div id="FillWindow">
          <div class="settings-text">Enlarge Display to Fill Window</div>
          <label class="tgl-switch">
            <input
              type="checkbox"
              id="enlarge-display-to-fill-window-tgl"
              class="tgl tgl-flat"
              checked
            />
            <div class="tgl-slider"></div>
          </label>
        </div>
        <div id="QualityControlOwnership">
          <div class="settings-text">Quality control ownership</div>
          <label class="tgl-switch">
            <input
              type="checkbox"
              id="quality-control-ownership-tgl"
              class="tgl tgl-flat"
            />
            <div class="tgl-slider"></div>
          </label>
        </div>
        <div id="statsSetting">
          <div class="settings-text">Show Stats</div>
          <label class="tgl-switch">
            <input
              type="checkbox"
              id="show-stats-tgl"
              class="tgl tgl-flat"
              checked
            />
            <div class="tgl-slider"></div>
          </label>
          <div id="statsContainer">
            <div id="stats"></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { load, onParagonLoad } from "../UE4Player/app";
export default {
  mounted() {
    load();
    onParagonLoad();
  }
};
</script>

<style>
#statsContainer {
  background-color: rgba(0, 0, 0, 0.8);
  text-align: left;
  display: block;
}

#stats {
  font-size: 14px;
  font-weight: bold;
  padding: 6px;
  color: lime;
}

canvas {
  image-rendering: crisp-edges;
  position: absolute;
}

video {
  /* position: absolute; */
  width: 100%;
  height: 100%;
}

#player {
  width: 1280px;
  height: 720px;
  position: relative;
  background-color: #000;
}

#overlay {
  -moz-border-radius-bottomright: 5px;
  -moz-border-radius-bottomleft: 5px;
  -webkit-border-bottom-right-radius: 5px;
  -webkit-border-bottom-left-radius: 5px;
  border-bottom-right-radius: 5px; /* future proofing */
  border-bottom-left-radius: 5px; /* future proofing */
  -khtml-border-bottom-right-radius: 5px; /* for old Konqueror browsers */
  -khtml-border-bottom-left-radius: 5px; /* for old Konqueror browsers */

  -webkit-touch-callout: none; /* iOS Safari */
  -webkit-user-select: none; /* Safari */
  -khtml-user-select: none; /* Konqueror HTML */
  -moz-user-select: none; /* Firefox */
  -ms-user-select: none; /* Internet Explorer/Edge */
  user-select: none; /* Non-prefixed version, currently
                                  supported by Chrome and Opera */

  position: absolute;
  padding: 4px;
  top: 0;
  right: 2%;
  z-index: 100;
  border: 2px solid var(--colour4);
  border-top-width: 0px;
}

.overlay {
  background-color: var(--colour2);
  font-family: var(--buttonFont);
  font-weight: lighter;
  color: var(--colour4);
}

.overlay-shown > #overlaySettings {
  padding: 50px 4px 4px 4px;
  display: block;
}

.overlay-shown > div > #overlayButton {
  transform: rotate(-135deg);
  -webkit-transform: rotate(-135deg); /* Safari */
  -moz-transform: rotate(-135deg); /* Firefox */
  -ms-transform: rotate(-135deg); /* IE */
  -o-transform: rotate(-135deg); /* Opera */
}

#overlayButton:hover {
  cursor: pointer;
}

#overlayButton {
  transition-duration: 250ms;
  float: right;
  text-align: right;
  font-size: 40px;
}

#qualityStatus {
  float: left;
  font-size: 37px;
  padding-right: 4px;
}

#overlaySettings {
  width: 300px;
  display: none;
}

.greyStatus {
  color: grey;
}

.limeStatus {
  color: lime;
}

.orangeStatus {
  color: orange;
}

.redStatus {
  color: red;
}

#videoMessageOverlay {
  z-index: 20;
  color: var(--colour4);
  font-size: 1.8em;
  position: absolute;
  margin: auto;
  font-family: var(--inputFont);
  width: 100%;
}

#videoPlayOverlay {
  z-index: 30;
  position: absolute;
  color: var(--colour4);
  font-size: 1.8em;
  font-family: var(--inputFont);
  width: 100%;
  height: 100%;
  background-color: rgba(100, 100, 100, 0.7);
}

/* State for element to be clickable */
.clickableState {
  align-items: center;
  justify-content: center;
  display: flex;
  cursor: pointer;
}

/* State for element to show text, this is for informational use*/
.textDisplayState {
  display: flex;
}

/* State to hide overlay, WebRTC communication is in progress and or is playing */
.hiddenState {
  display: none;
}

#playButton {
  display: inline-block;
  height: auto;
}

img#playButton {
  max-width: 241px;
  width: 10%;
}

#UIInteraction {
  position: fixed;
}

#UIInteractionButtonBoundary {
  padding: 2px;
}

#UIInteractionButton {
  cursor: pointer;
}

#hiddenInput {
  position: absolute;
  left: -10%; /* Although invisible, push off-screen to prevent user interaction. */
  width: 0px;
  opacity: 0;
}

#editTextButton {
  position: absolute;
  height: 40px;
  width: 40px;
}

.settings-text {
  color: var(--colour4);
  vertical-align: middle;
  font-size: 18px;
  font-weight: normal;
  display: inline-block;
}

.overlay-button {
  line-height: 1.1;
  padding: 1px 6px;
}

.btn-overlay {
  float: right;
  vertical-align: middle;
  display: inline-block;
}

.btn-flat {
  background: var(--colour4);
  border: 2px solid var(--colour5);
  font-weight: bold;
  cursor: pointer;
  font-family: var(--buttonFont);
  font-size: 10px;
  color: var(--colour5);
  border-radius: 5px;
  height: 17px;
}

.btn-flat:disabled {
  background: var(--colour4);
  border-color: var(--colour3);
  color: var(--colour3);
  cursor: default;
}

.btn-flat:active {
  border-color: var(--colour2);
  color: var(--colour2);
}

.btn-flat:focus {
  outline: none;
}
/*** Toggle Switch styles ***/
.tgl-switch {
  float: right;
  vertical-align: middle;
  display: inline-block;
}

.tgl-switch .tgl {
  display: none;
}

.tgl,
.tgl:after,
.tgl:before,
.tgl *,
.tgl *:after,
.tgl *:before,
.tgl + .tgl-slider {
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}
.tgl::-moz-selection,
.tgl:after::-moz-selection,
.tgl:before::-moz-selection,
.tgl *::-moz-selection,
.tgl *:after::-moz-selection,
.tgl *:before::-moz-selection,
.tgl + .tgl-slider::-moz-selection {
  background: none;
}
.tgl::selection,
.tgl:after::selection,
.tgl:before::selection,
.tgl *::selection,
.tgl *:after::selection,
.tgl *:before::selection,
.tgl + .tgl-slider::selection {
  background: none;
}

.tgl + .tgl-slider {
  outline: 0;
  display: block;
  width: 40px;
  height: 18px;
  position: relative;
  cursor: pointer;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.tgl + .tgl-slider:after,
.tgl + .tgl-slider:before {
  position: relative;
  display: block;
  content: "";
  width: 50%;
  height: 100%;
}
.tgl + .tgl-slider:after {
  left: 0;
}
.tgl + .tgl-slider:before {
  display: none;
}

.tgl-flat + .tgl-slider {
  padding: 2px;
  -webkit-transition: all 0.2s ease;
  transition: all 0.2s ease;
  background: #fff;
  border: 3px solid var(--colour4);
  border-radius: 2em;
}

.tgl-flat + .tgl-slider:after {
  -webkit-transition: all 0.2s ease;
  transition: all 0.2s ease;
  background: var(--colour4);
  content: "";
  border-radius: 1em;
}

.tgl-flat:checked + .tgl-slider {
  border: 3px solid var(--colour5);
}

.tgl-flat:checked + .tgl-slider:after {
  left: 50%;
  background: var(--colour5);
}
/*** Toggle Switch styles ***/
</style>
