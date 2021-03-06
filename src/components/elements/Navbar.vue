<template>
  <div id="Navbar" class="nav">
    <div class="logo" v-on:click="homeNav"></div>
    <div v-on:click="navToggle" class="navButton">
      <center><div v-bind:class="navbutton" class="navButtonIcon"></div></center>
    </div>
    <div v-bind:class="navpane" class="navpane">
      <center>
        <div v-on:click="loginNav" v-bind:class="login">Login</div>
        <div v-on:click="registerNav" v-bind:class="login">Register</div>
        <div v-on:click="accountNav" v-bind:class="logged">Account</div>
        <div v-on:click="timeClockNav" v-bind:class="logged">Time Clock</div>
        <div v-on:click="jobsNav" v-bind:class="logged">Jobs</div>
        <div v-on:click="leadsNav" v-bind:class="logged">Leads</div>
        <div v-on:click="scheduleNav" v-bind:class="logged">Schedule</div>
        <div v-on:click="locationNav" v-bind:class="logged">Location</div>
        <div v-on:click="messagingNav" v-bind:class="logged">Messaging</div>
        <div v-on:click="logOut" v-bind:class="logged">Log Out</div>
      </center>
    </div>
  </div>
</template>

<script>
  var x = false
  export default {
    name: 'Navbar',
    data: function () {
      return {
        isToggled: false,
        first: true
      }
    },
    props: ['loggedNav'],
    computed: {
      navbutton: function () {
        return {
          navButtonAnimation: this.isToggled,
          navButtonAnimationExit: !this.isToggled && !this.first
        }
      },
      navpane: function () {
        return {
          navpaneAnimation: this.isToggled,
          navpaneAnimationExit: !this.isToggled && !this.first
        }
      },
      about: function () {
        return {
          navtileAnimation: this.isToggled,
          navtileAnimationExit: !this.isToggled && !this.first,
          navtile: true
        }
      },
      login: function () {
        return {
          hidden: this.loggedNav,
          navtileAnimation: this.isToggled,
          navtileAnimationExit: !this.isToggled && !this.first,
          navtile: !this.loggedNav
        }
      },
      logged: function () {
        return {
          hidden: !this.loggedNav,
          navtileAnimation: this.isToggled,
          navtileAnimationExit: !this.isToggled && !this.first,
          navtile: this.loggedNav
        }
      }
    },
    methods: {
      navToggle: function () {
        // Nav button functionality
        if (x === false) {
          x = true
          this.isToggled = true
          this.first = false
        }
        else if (x === true) {
          x = false
          this.isToggled = false
        }
      },
      homeNav: function () {
        if (this.loggedNav === false) {
          this.$router.push('/login')
        }
        else {
          this.$router.push('/account')
        }
        this.isToggled = false
        x = false
        clearInterval()
      },
      loginNav: function () {
        this.$router.push('/login')
        this.isToggled = false
        x = false
        clearInterval()
      },
      registerNav: function () {
        this.$router.push('/register')
        this.isToggled = false
        x = false
        clearInterval()
      },
      accountNav: function () {
        this.$router.push('/account')
        this.isToggled = false
        x = false
        clearInterval()
      },
      timeClockNav: function () {
        this.$router.push('/timeclock')
        this.isToggled = false
        x = false
        clearInterval()
      },
      jobsNav: function () {
        this.$router.push('/jobs')
        this.isToggled = false
        x = false
        clearInterval()
      },
      leadsNav: function () {
        this.$router.push('/leads')
        this.isToggled = false
        x = false
        clearInterval()
      },
      scheduleNav: function () {
        this.$router.push('/schedule')
        this.isToggled = false
        x = false
        clearInterval()
      },
      locationNav: function () {
        this.$router.push('/location')
        this.isToggled = false
        x = false
        clearInterval()
      },
      messagingNav: function () {
        this.$router.push('/messaging')
        this.isToggled = false
        x = false
        clearInterval()
      },
      logOut: function () {
        this.isToggled = false
        x = false
        this.$emit('logOut')
        clearInterval()
      }
    }
  }
  // prevents safari greying linking divs on tap
  document.addEventListener('touchstart', function () {}, true)
</script>

<style scoped lang="less">
  @backgroundColor: #355477;
  @secondaryColor: #1a222e;
  @paymentColor: #519d10;
  @medicalColor: #ee1f34;
  @dark: #161817;
  @light: #6b6b6b;
  @darkTR: #000;
  @lightTR: #444;
  @textColor: #9fb0d6;
  @baseFontSize: 1em;
  @boldText: "tahoma";
  @sideText: "AdventPro";
  @bodyText: "LiberationSans";

  .nav {
    height: 80px;
    background: #161817;
    background-image: -webkit-linear-gradient(top, @light, @dark);
    background-image: -moz-linear-gradient(top, @light, @dark);
    background-image: -ms-linear-gradient(top, @light, @dark);
    background-image: -o-linear-gradient(top, @light, @dark);
    background-image: linear-gradient(to bottom, @light, @dark);
    display: grid;
    grid-template-columns: 10px repeat(5, 1fr) 10px;
    z-index: 2;
    box-shadow: 0px 6px 2px #d1d1d1;
  }

  .logo {
    background-image: url('../../assets/carpetguytype.png');
    background-repeat: no-repeat;
    grid-column-start: 1;
    grid-column-end: 4;
    grid-row: 1;
    line-height: 80px;
    margin-top: 10px;
    height: 80px;
    width: 270px;
    transform: scale(.80,.80)
  }

  .navButton {
    grid-column: 6;
    width: 100px;
    height: 100px;
    transform: scale(.75,.75);
    -webkit-tap-highlight-color: rgba(0,0,0,0);
  }

  .navButtonIcon {
    width: 80px;
    height: 80px;
    background: url("../../assets/navbuttonAnimationWhite.svg");
    background-repeat: no-repeat;
  }

  .navpane {
    position: absolute;
    top: -2000px;
    width: 100%;
    z-index: 3;
  }

  .navtile {
    width: 90%;
    height: 40px;
    line-height: 25px;
    border-radius: 10px;
    margin: 10px 0;
    padding: 4px;
    background: #0c2069;
      background-image: -webkit-linear-gradient(top, @dark, @light);
      background-image: -moz-linear-gradient(top, @dark, @light);
      background-image: -ms-linear-gradient(top, @dark, @light);
      background-image: -o-linear-gradient(top, @dark, @light);
      background-image: linear-gradient(to bottom, @dark, @light);
    text-align: center;
    font-family: @boldText;
    font-size: @baseFontSize + 1em;
    text-decoration: none;
    color: #FFF;
    border: 2px solid #fff;
    z-index: 3;
  }

  .hidden {
    display: none;
  }

  @keyframes activateNav {
    from {top: -2000px;}
    to {top: 90px;}
  }

  @keyframes activateNavtiles {
    0% {margin: 10px 0;}
    40% {margin: 22px 0;}
    80% {margin: 12px 0;}
    100% {margin: 12px 0;}
  }

  @keyframes deactivateNav {
    0% {top: 80px;}
    99% {top: 2000px;}
    100% {display: none;}
  }

  @keyframes deactivateNavtiles {
    0% {margin: 12px 0;}
    50% {margin: 18px 0;}
    100% {margin: 26px 0;}
  }

  @keyframes navButtonAnimation {
    100% {background-position: -1440px;}
  }

  @keyframes navButtonAnimationReverse {
    0% {background-position: -1440px;}
    100% {background-position: 0px;}
  }

  .navpaneAnimation {
    animation-name: activateNav;
    animation-duration: .8s;
    animation-iteration-count: 1;
    animation-fill-mode: forwards;
    display: inline;
  }

  .navtileAnimation {
    animation-name: activateNavtiles;
    animation-duration: 1.5s;
    animation-iteration-count: 1;
    animation-fill-mode: forwards;
  }

  .navpaneAnimationExit {
    animation-name: deactivateNav;
    animation-duration: 1.5s;
    animation-iteration-count: 1;
    animation-fill-mode: forwards;
  }

  .navtileAnimationExit {
    animation-name: deactivateNavtiles;
    animation-duration: 1.5s;
    animation-iteration-count: 1;
    animation-fill-mode: forwards;
  }

  .navButtonAnimation {
    animation: navButtonAnimation .4s steps(18);
    animation-iteration-count: 1;
    animation-fill-mode: forwards;
  }

  .navButtonAnimationExit {
    animation: navButtonAnimationReverse .5s steps(18);
    animation-iteration-count: 1;
    animation-fill-mode: forwards;
  }

  a {
    text-decoration: none;
  }

</style>
