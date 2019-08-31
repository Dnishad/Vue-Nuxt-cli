<template>
  <div>
  <nav class="navbar navbar-expand-lg navbar-dark bg-transparent">
    <a class="navbar-brand">F</a>
    <button
      class="navbar-toggler custom-toggler"
      type="button"
      data-toggle="collapse"
      data-target="#navbarSupportedContent"
      aria-controls="navbarSupportedContent"
      aria-expanded="false"
      aria-label="Toggle navigation"
    >
      <span class="navbar-toggler-icon"></span>
    </button>

    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav mr-auto snip1155">
        <li class="nav-item">
          <a class="nav-link">
            Home
            <span class="sr-only">(current)</span>
          </a>
        </li>
        <li class="nav-item">
          <a class="nav-link">
            About Us
            <span class="sr-only">(current)</span>
          </a>
        </li>
        <li class="nav-item">
          <a class="nav-link">
           Help
            <span class="sr-only">(current)</span>
          </a>
        </li>
      </ul>
      <ul class="nav navbar-nav navbar-right snip1155">
        <li class="nav-item">
          <a class="nav-link">
           Blog
            <span class="sr-only">(current)</span>
          </a>
        </li>
        <!-- <button type="button" class="btn btn-default btn-circle custom-toggler">
       <span class="navbar-toggler-icon"></span>
        </button>-->
      </ul>
    </div>
  </nav>
  </div>
</template>
<script>
export default {
  mounted() {
    var btn = document.querySelectorAll("li");
    var ctx;
    [...btn].forEach(btn => {
      html2canvas(btn).then(canvas => {
        ctx = canvas.getContext("2d");
        createParticleCanvas();
        let reductionFactor = 17;
        btn.addEventListener("click", e => {
          let width = btn.offsetWidth;
          let height = btn.offsetHeight;
          let colorData = ctx.getImageData(0, 0, width, height).data;
          let count = 0;

          for (let localX = 0; localX < width; localX++) {
            for (let localY = 0; localY < height; localY++) {
              if (count % reductionFactor === 0) {
                let index = (localY * width + localX) * 4;
                let rgbaColorArr = colorData.slice(index, index + 4);

                let bcr = btn.getBoundingClientRect();
                let globalX = bcr.left + localX;
                let globalY = bcr.top + localY;

                createParticleAtPoint(globalX, globalY, rgbaColorArr);
              }
              count++;
            }
          }
        });
      });

      var ExplodingParticle = function() {
        this.animationDuration = 1000; // in ms
        this.speed = {
          x: -5 + Math.random() * 10,
          y: -5 + Math.random() * 10
        };

        this.radius = 5 + Math.random() * 5;

        this.life = 30 + Math.random() * 10;
        this.remainingLife = this.life;

        this.draw = ctx => {
          let p = this;

          if (this.remainingLife > 0 && this.radius > 0) {
            ctx.beginPath();
            ctx.arc(p.startX, p.startY, p.radius, 0, Math.PI * 2);
            ctx.fillStyle = "rgba( 248,249,250 , 1)";
            ctx.fill();

            p.remainingLife--;
            p.radius -= 0.25;
            p.startX += p.speed.x;
            p.startY += p.speed.y;
          }
        };
      };

      var particles = [];
      function createParticleAtPoint(x, y, colorData) {
        let particle = new ExplodingParticle();
        particle.rgbArray = colorData;
        particle.startX = x;
        particle.startY = y;
        particle.startTime = Date.now();

        particles.push(particle);
      }

      var particleCanvas, particleCtx;
      function createParticleCanvas() {
        particleCanvas = document.createElement("canvas");
        particleCtx = particleCanvas.getContext("2d");

        particleCanvas.width = window.innerWidth;
        particleCanvas.height = window.innerHeight;

        particleCanvas.style.position = "absolute";
        particleCanvas.style.top = "0";
        particleCanvas.style.left = "0";

        particleCanvas.style.zIndex = "1001";

        particleCanvas.style.pointerEvents = "none";

        document.body.appendChild(particleCanvas);
      }

      function update() {
        if (typeof particleCtx !== "undefined") {
          particleCtx.clearRect(0, 0, window.innerWidth, window.innerHeight);
        }

        for (let i = 0; i < particles.length; i++) {
          particles[i].draw(particleCtx);

          if (i === particles.length - 1) {
            let percent =
              (Date.now() - particles[i].startTime) /
              particles[i].animationDuration;

            if (percent > 1) {
              particles = [];
            }
          }
        }

        window.requestAnimationFrame(update);
      }
      window.requestAnimationFrame(update);
    });
  }
};
</script>
<style>
@import url("https://fonts.googleapis.com/css?family=Raleway:400,500");
@import url("https://fonts.googleapis.com/css?family=Sacramento");
.btn {
  cursor: pointer;
  background: #f8f9fa;
  width: 40px;
  height: 40px;
  padding: 6px 5px;
  border-radius: 43px;
}
.custom-toggler {
  width: 40px;
  height: 40px;
  padding: 6px 5px;
  background-color: white;
}
.custom-toggler .navbar-toggler-icon {
  background-image: url("data:image/svg+xml;charset=utf8,%3Csvg viewBox='0 0 32 32' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath stroke='rgba(0, 0, 0)' stroke-width='2' stroke-linecap='round' stroke-miterlimit='10' d='M4 8h24M4 16h24M4 24h24'/%3E%3C/svg%3E");
}
.navbar-brand {
  font-family: "Sacramento", cursive;
  color: white !important;
  font-weight: 900;
  font-size: 20px;
  margin-left: 30px;
  border: solid 2px;
  padding: 6px 8px 3px 6px;
}
.navbar {
  /* min-height: 110px; */
  position: absolute;
  width:100%
}
.snip1155 {
  font-family: "Raleway", Arial, sans-serif;
  text-align: center;
  text-transform: uppercase;
  font-weight: 500;
}
.snip1155 * {
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  -webkit-transition: all 0.35s ease;
  transition: all 0.35s ease;
}
.snip1155 li {
  display: inline-block;
  list-style: outside none none;
  margin: 0 2em;
  padding: 0;
}
.snip1155 a {
  display: inline-block;
  padding: 0.5em 17px;
  color: rgba(255, 255, 255, 0.5);
  position: relative;
  letter-spacing: 1px;
  text-decoration: none;
}
.snip1155 a:before {
  left: 20%;
  right: 20%;
  top: 50%;
  content: "";
  border-left: 16px solid #f8f9fa;
  border-right: 16px solid #f8f9fa;
  -webkit-transform: translateY(-50%);
  transform: translateY(-50%);
  height: 3px;
  opacity: 0;
  position: absolute;
  -webkit-transition: all 0.35s ease;
  transition: all 0.35s ease;
}
.snip1155 a:hover,
.snip1155 .current a {
  color: #ffffff;
}
.snip1155 a:hover:before,
.snip1155 .current a:before {
  left: 0;
  right: 0;
  transform: rotate(-50deg);
  opacity: 1;
}

.navbar-dark .navbar-nav .nav-link {
  color: #f8f9fa;
  text-transform: uppercase;
  font-size: 13px;
  cursor: pointer;
}
</style>