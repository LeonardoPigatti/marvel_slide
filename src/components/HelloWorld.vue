<template>
  <article class="slider slider--active-1">
    <h2 style="z-index: 2; color: white; top: 150px; position: relative; text-transform: uppercase; font-style: italic;" class="h2 h2--top">Guardians of the Galaxy Heroes</h2>
    <section style="background-color: #475A51;" class="slider__slide slide slide--1">
      <h2 style="z-index: 2;" class="h2 h2--top">I am</h2>
      <img style="z-index: 2; cursor: pointer;" @click="toggleDiv" class="slide__img" src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/108082/groot.png" alt="Groot">
      <h2 style="z-index: 2;" class="h2 h2--bottom">Groot</h2>
      <h2  v-if="isDivVisible" style="z-index: 2; top: 250px; font-size: 20px !important; margin-left: 50px; font-style: italic;"  class="h2 p--bottom">Come meet me</h2>
      <div class="leo" v-if="isDivVisible">{{ Grootmessage }}</div>
    </section>
    <section style="background-color: #935c44;" class="slider__slide slide slide--2">
      <h2 style="z-index: 2;" class="h2 h2--top">Rocket</h2>
      <img style="z-index: 2; cursor: pointer;" @click="toggleDiv" class="slide__img" src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/108082/raccoon.png" alt="Raccoon">
      <h2 style="z-index: 2;" class="h2 h2--bottom">Raccoon</h2>
      <h2  v-if="isDivVisible" style="z-index: 2; top: 250px; font-size: 20px !important; margin-left: 50px; font-style: italic;"  class="h2 p--bottom">Come meet me</h2>
      <div class="leo" v-if="isDivVisible">{{ Racoonmessage }}</div>

    </section>
    <nav class="slider__navigation navigation">
      <a @click="leoz" href="javascript:void(0);" class="navigation__item nav nav--1">
        <div class="nav__border">
          <div style="background-color: #475A51;" class="img img--color-1">
            <img class="nav__img" src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/108082/groot.png" alt="Groot">
          </div>
        </div>
      </a>
      <a @click="leoz" style="background-color: #935c44;" href="javascript:void(0);" class="navigation__item nav nav--2">
        <div class="nav__border">
          <div class="img img--color-2">
            <img class="nav__img" src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/108082/raccoon.png" alt="Raccoon">
          </div>
        </div>
      </a>
    </nav>
    <i class="bg-slide"></i>
  </article>
  </template>
  
  <script>
  import $ from 'jquery';
  
  export default {
    name: 'HelloWorld',
    props: {
      msg: String
    },
    mounted() {
      $(function() {
        var slider = $('.slider');
        var slide = $('.slide');
        var nav = $('.nav');
  
        slide.each(function(index) {
          var $this = $(this);
          $this.attr('data-slide', index + 1);
        });
        
        nav.each(function(index) {
          var $this = $(this);
          $this.attr('data-item', index + 1);
        });
        
        nav.on('click', function(e) {
          e.preventDefault();
          
          var $this = $(this);
          var itemNav = $this.data('item');
          var prevSlide = itemNav - 1;
          var a, b;
          
          if (itemNav == 1) {
            a = nav.length;
            b = 1;
          } else {
            a = prevSlide;
            b = itemNav;
          }
          slider.addClass('slider--back').delay(600).queue(function(){
            $(this).removeClass('slider--active-'+a)
              .addClass('slider--active-'+b)
              .addClass('slider--delay')
              .dequeue();
          }).delay(400).queue(function() {
            $(this).removeClass('slider--back')
            .dequeue();
          }).delay(400).queue(function(){
            $(this).removeClass('slider--delay')
            .dequeue();
          });
        });
      });
    },
  
    data() {
      return {
        isDivVisible: false,
        Grootmessage: 'Hailing from the Branch Worlds’ Planet X, Groot is part of a species called Groot, so his name is also the title of his taxonomic classification. From the time he was a sapling, Groot was destined to protect the rights of the downtrodden. He campaigned for the Undergrowth, anthropomorphic animals and fungi who helped maintain Planet X’s ecosystem by performing menial tasks. Groot’s noble campaign drew the rancor of the other Groots and he ended up leaving his home world.',
        Racoonmessage: 'Imagine if your average raccoon suddenly gained a PhD in engineering and a penchant for sarcasm. That’s Rocket Raccoon for you. Hailing from the far-flung reaches of the Marvel universe, Rocket is a raccoon with a chip on his shoulder and a laser gun in his hand. He’s not just a raccoon; he’s a raccoon with a flair for intergalactic mischief and an uncanny knack for mechanics.',
      };
    },

    methods: {
      toggleDiv() {
    this.isDivVisible = !this.isDivVisible;
    const button = document.querySelector('.button-2');
    button.classList.toggle('active');
  },
  leoz() {
    this.isDivVisible = false;
  }
  }
  }
  </script>
    
  <style lang="scss" scoped>
  @import url("https://fonts.googleapis.com/css?family=Inconsolata:400,700");
  
  @mixin size($width, $height: $width) {
    width: $width;
    height: $height;
  }
  
  @mixin center-absolute($top: false) {
    position: absolute;
    top: 50%;
    @if ($top == false) {
      left: 50%;
      transform: translate(-50%, -50%);
    } @else {
      transform: translateY(-50%);
    }
  }
  
  * {
    box-sizing: border-box;
  }
  
  $var: '--';
  $min-slide: 1;
  $max-slide: 2;
  $all-colors-main: (
    'white': #fff
  );
  $all-colors-slide: (
    2: #935c44, 
    1: #475a51, 
    3: #49c5b6 
  );
  $size-nav: 100px;
  
  :root {
    @for $i from $min-slide through $max-slide {
      #{$var}color-#{$i}: map-get($all-colors-slide, $i);
    }
  }
  
  body {
    font-family: Inconsolata, serif;
    overflow: hidden;
  }
  
  
  .leo {
    height: 285px;
    z-index: 2;
    width: 80%;
    max-width: 600px;
    padding: 20px;
    margin: 0 auto;
    background: rgba(255, 255, 255, 0.1);
    border-radius: 10px;
    border: 2px solid rgba(255, 255, 255, 0.3);
    font-family: "Montserrat", sans-serif;
    font-size: 1.2em;
    line-height: 1.6;
    color: #fff;
    text-align: justify;
    text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.5);
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    position: relative;
    top: 50%;
    transform: translateY(-70%) translateX(350px);
    
  }

  .button-2 {
  position: relative;
  background-color: white;
  color: black; 
  border: 2px solid black; 
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s, color 0.3s, transform 0.3s;
  border-radius: 5px;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 2;
  
  
  top: 250px;
  left: 1105px; 
  transform: translateX(-50%); 

  .button-icon {
    width: 54px; 
    height: 54px; 
    border-left: 22.5px solid transparent; 
    border-right: 22.5px solid transparent; 
    border-top: 36px solid black; 
    margin-right: 45px; 
    transition: transform 0.3s ease;
}
  &.active {
    background-color: black;
    border-color: black;
    color: #fff; 
    
    .button-icon {
      transform: rotate(180deg);
      color: #fff;
      border-top: 36px solid white;

    }
  }
}
  
  .slider {
    position: relative;
    @include size(100vw, 100vh);
    overflow: hidden;
    .slide {
      opacity: 0;
      position: absolute;
      @include size(100%);
      overflow: hidden;
      transition: all 0.1s ease 0.2s;
      @for $i from $min-slide through $max-slide {
        &--#{$i} {
          background: var(--color-#{$i});
        }
      }
      &__img {
        user-select: none;
        position: absolute;
        bottom: 0;
        left: calc(50% - 100px);
        height: 80vh;
        transform: translateX(-50%) scale(1.3);
        opacity: 0;
        transition: all 1s ease;
      }
      .h2 {
        user-select: none;
        display: inline-block;
        position: absolute;
        left: 50%;
        margin: 0;
        text-transform: uppercase;
        letter-spacing: 2px;
        color: map-get($all-colors-main, 'white');
        font-size: 7vw;
        transition: all 1s ease;
        @media (max-width: 768px) {
          font-size: 86px;
        }
        @media (max-width: 414px) and (min-width: 321px) {
          font-size: 45px;
        }
        @media (max-width: 320px) {
          font-size: 35px;
        }
        &:after {
          display: block;
          content: '';
          position: absolute;
          top: 0;
          left: 0;
          right: 0;
          height: 98%;
          background-color: map-get($all-colors-main, 'white');
          transition: all 0.5s ease 1.3s;
        }
        &--top {
          top: 40%;
          transform: translateX(-300%);
          @media (max-width: 768px) {
            top: 10%;
          }
        }
        &--bottom {
          top: 60%;
          transform: translateX(100%);
          @media (max-width: 768px) {
            top: 20%;
          }
        }
      }
    }
    .navigation {
      @include center-absolute(true);
      margin-top: -4%;
      right: 200px;
      @media (max-width: 414px) {
        right: 120px;
      }
      &__item {
        -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
        -webkit-tap-highlight-color: transparent;
        user-select: none;
        position: absolute;
        display: flex;
        justify-content: center;
        align-items: center;
        @include size($size-nav);
        border-radius: 50%;
        border: 1px solid map-get($all-colors-main, 'white');
        transform: scale(0);
        transition: all 0.3s ease 0.3s;
        .nav__border {
          position: relative;
          @include size($size-nav - 25px);
          box-shadow: 1px 1px 8px 0 rgba(0, 0, 0, 0.3);
          border-radius: inherit;
          transform: scale(1);
          transition: all 0.6s ease;
          overflow: hidden;
          .img {
            user-select: none;
            @include center-absolute;
            @include size($size-nav);
            border-radius: inherit;
            img {
              width: $size-nav;
              user-select: none;
            }
            @for $i from $min-slide through $max-slide {
              &--color-#{$i} {
                background-color: var(--color-#{$i});
              }
            }
          }
        }
        &:focus,
        &:active {
          outline: none;
          user-select: none;
        }
      }
    }
    .bg-slide {
      content: '';
      display: block;
      @include center-absolute(true);
      margin-top: 0;
      right: 120px;
      @include size(0);
      border-radius: 50%;
      opacity: 0;
      transition: width 0.8s ease 0.2s, height 0.8s ease 0.2s, right 0.8s ease 0.2s, opacity 0.3s ease;
      @media (max-width: 414px) {
        margin-top: 30px;
      }
    }
  
    @for $i from $min-slide through $max-slide {
      &--active-#{$i} {
        @if ($i + 1 > $max-slide) {
          .nav--1 {
            transform: scale(1);
          }
        } @else {
          .nav--#{$i + 1} {
            transform: scale(1);
          }
        }
        .slide--#{$i} {
          opacity: 1;
          .slide__img {
            transform: translateX(-50%) scale(1.1);
            opacity: 1;
            @media (max-width: 414px) {
              transform: translateX(-40%) scale(1.1);
            }
          }
          .h2--top {
            transform: translateX(-150%);
            @media (max-width: 768px) {
              transform: translateX(-115%);
            }
            &:after {
              right: 100%;
            }
          }
          .h2--bottom {
            transform: translateX(0%);
            &:after {
              left: 100%;
            }
          }
          .p--top {
            transform: translateX(-150%);
            @media (max-width: 768px) {
              transform: translateX(-115%);
            }
            &:after {
              right: 100%;
            }
          }
          .p--bottom {
            transform: translateX(0%);
            &:after {
              left: 100%;
            }
          }
        }
        .bg-slide {
          &:not(.slider--back) {
            @if ($i + 1 > $max-slide) {
              background-color: var(--color-1);
            } @else {
              background-color: var(--color-#{$i + 1});
            }
          }
          &--#{$i} {
            @include size(0);
            opacity: 0;
            right: 120px;
            @media (max-width: 414px) {
              right: 80px;
            }
          }
        }
      }
    }
  
    &.slider--back {
      @for $i from $min-slide through $max-slide {
        &.slider--active-#{$i} {
          .slide__img {
            transform: translateX(-50%) scale(1.3);
            opacity: 0;
          }
          .h2--top {
            transform: translateX(-300%);
          }
          .h2--bottom {
            transform: translateX(100%);
          }
          .p--top {
            transform: translateX(-300%);
          }
          .p--bottom {
            transform: translateX(100%);
          }
          .bg-slide {
            right: -120px;
            @include size(200vw);
            opacity: 1;
          }
          .nav__border {
            transform: scale(1.25);
          }
        }
      }
    }
    &.slider--delay {
      @for $i from $min-slide through $max-slide {
        &.slider--active-#{$i} {
          .bg-slide {
            background-color: var(--color-#{$i});
          }
        }
      }
    }
  }
  </style>
  