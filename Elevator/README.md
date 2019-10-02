# Project1
first project for Emerging Media

<<<<<<< HEAD
Ok, I am editing the README


Pineapple

Luis wishes he is a pretty pineapple
=======
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>A-Frame Test</title>
    <meta name="description" content="">
    <meta name="author" content="leo">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <script src="https://aframe.io/releases/0.9.2/aframe.min.js"></script>
  </head>
  <body>
    <script>
        AFRAME.registerComponent('play-on-vrdisplayactivate-or-enter-vr', {
          init: function () {
            this.playVideo = this.playVideo.bind(this);
            this.playVideoNextTick = this.playVideoNextTick.bind(this);
          },
          play: function () {
            window.addEventListener('vrdisplayactivate', this.playVideo);
            this.el.sceneEl.addEventListener('enter-vr', this.playVideoNextTick);
          },
          pause: function () {
            this.el.sceneEl.removeEventListener('enter-vr', this.playVideoNextTick);
            window.removeEventListener('vrdisplayactivate', this.playVideo);
          },
          playVideoNextTick: function () {
            setTimeout(this.playVideo);
          },
          playVideo: function () {
            var video = this.el.components.material.material.map.image;
            if (!video) { return; }
            video.play();
          }
      });
      
      AFRAME.registerComponent('play-on-window-click', {
        init: function () {
          this.onClick = this.onClick.bind(this);
        },
        play: function () {
          window.addEventListener('click', this.onClick);
        },
        pause: function () {
          window.removeEventListener('click', this.onClick);
        },
        onClick: function (evt) {
          var video = this.el.components.material.material.map.image;
          if (!video) { return; }
          video.play();
        }
      });
      
      AFRAME.registerComponent('rotator', {
        tick: function(time, timeDelta) {
          let currentPos = this.el.getAttribute('rotation');
          this.el.setAttribute('rotation', {
            x: currentPos.x + timeDelta * 0.1,
            y: currentPos.y + timeDelta * 0.1,
            z: currentPos.z + timeDelta * 0.1
          });
        }
      });
      
      AFRAME.registerComponent('teleport', {
        schema: {target: {type: 'string', default: '#main'}},
        
        init: function() {
          let t = this.data.target;
          this.el.addEventListener('click', function(){
             alert("The magic box takes you to places");
             let vs = document.querySelector('a-videosphere');
             vs.setAttribute('interactive-video', {src: t});
          })
        }
      });
      
      AFRAME.registerComponent('interactive-video', {
        schema: {src: {type: 'string', default: '#main'}},
        
        init: function() {
          this.el.setAttribute('src', '#main');
        },
        
        update: function() {
          this.el.setAttribute('src', this.data.src);
          let triggers = document.querySelectorAll('.raycast-target');
          for (let trigger of triggers) {
              trigger.setAttribute('visible', false);
              trigger.className = 'raycast-target-off';
          }
          triggers = document.querySelector(this.data.src + '-triggers').querySelectorAll('.raycast-target-off');
          for (let trigger of triggers) {
              trigger.setAttribute('visible', true);
              trigger.className = 'raycast-target';
          }
        }
      });
      
    </script>
    <a-scene background="color: #FAFAFA">      
      <a-camera wasd-controls="enabled: false">
            <a-entity id="mycursor" cursor="fuse: true; fuseTimeout: 500; max-distance: 30;" raycaster="objects: .raycast-target" position="0 0 -0.5" geometry="primitive: ring; radiusInner: 0.015; radiusOuter: 0.018" material="color: white; shader: flat; opacity: 0.25"></a-entity>
      </a-camera> 
      
      <a-videosphere id="video" interactive-video play-on-window-click play-on-vrdisplayactivate-or-enter-vr></a-videosphere>
      
      <a-entity id="main-triggers">
             <a-box class="raycast-target" src="https://cdn.glitch.com/314dba45-7b7c-4834-9410-f90659352834%2FBOX%20TEXTURE.png?v=1569258881482" 
             height="0.5" depth="0.5" width="0.5" position="6 1.8 -0.1" rotation="45 45 45" material="color: #cccccc; opacity:0.8" 
             rotator teleport="target: #room1"></a-box>
      </a-entity>
      
      <a-entity id="room1-triggers">
            <a-box class="raycast-target" src="https://cdn.glitch.com/314dba45-7b7c-4834-9410-f90659352834%2FBOX%20TEXTURE.png?v=1569258881482" 
             height="0.5" depth="0.5" width="0.5" position="-8 1.8 -3" rotation="45 45 45" material="color: #cccccc; opacity:0.8" 
             rotator teleport="target: #main"></a-box>
      </a-entity>
      
      <a-entity id="room2-triggers">
      </a-entity>
      
      <a-entity id="room3-triggers">
      </a-entity>
      
      <a-entity id="secret-area-triggers">
      </a-entity>
      
    </a-scene>
    
    <a-assets>
      <video id="main" autoplay="true" loop="true" crossorigin="anonymous" playsinline webkit-playsinline>
        <source type="video/mp4" src="https://cdn.glitch.com/314dba45-7b7c-4834-9410-f90659352834%2FVideo_1_Medium.mp4?v=1570032165418"/>
      </video>
      
      <video id="room1" autoplay="true" loop="true" crossorigin="anonymous" playsinline webkit-playsinline>
        <source type="video/mp4" src="https://cdn.glitch.com/314dba45-7b7c-4834-9410-f90659352834%2FVideo_4_Medium.mp4?v=1570032221551"/>
      </video>
      
      <video id="room2">
      </video>
      
      <video id="room3">
      </video>
      
      <video id="secret-area">
      </video>
    </a-assets>
  </body> 
</html>
>>>>>>> 1f84b5ec235def8e9cd4b5b4dba4682fe6a51262
