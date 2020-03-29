<template>
  <section class="section">
    <div class="filter">
      <h4 class="filter__heading">
        {{ title }}
      </h4>
      <div class="filter__item">
        <button class="filter__button" v-bind:class="{'filter__button--active': selectedFilter === 'All'}"
                @click="selectAll()">All
        </button>
        <button class="filter__button" v-bind:class="{'filter__button--active': selectedFilter === 'Movie'}"
                @click="selectMovies()">Movies
        </button>
        <button class="filter__button" v-bind:class="{'filter__button--active': selectedFilter === 'TV-Show'}"
                @click="selectTvShows()">TV Shows
        </button>
        <div class="filter__icons">
          <svg class="filter__icon" v-bind:class="{'filter__icon--active': !listView }" @click="transformToCards()"
               version="1.1" id="Web_Site" xmlns="http://www.w3.org/2000/svg"
               xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px"
               viewBox="69.1 318.8 473.7 213.8" enable-background="new 69.1 318.8 473.7 213.8" xml:space="preserve">
            <path d="M172.1,532.6h-103V318.8h103V532.6z"/>
            <path d="M295.7,532.6h-103V318.8h103V532.6z"/>
            <path d="M419.3,532.6h-103V318.8h103V532.6z"/>
            <path d="M542.9,532.6h-103V318.8h103V532.6z"/>
          </svg>
          <svg class="filter__icon" v-bind:class="{'filter__icon--active': listView }" @click="transformToList()"
               version="1.1" id="Web_Site" xmlns="http://www.w3.org/2000/svg"
               xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px"
               viewBox="69.1 318.7 473.7 214" enable-background="new 69.1 318.7 473.7 214" xml:space="preserve">
            <rect x="69.1" y="501.9" width="35.7" height="30.7"/>
            <rect x="69.1" y="440.8" width="35.7" height="30.7"/>
            <rect x="69.1" y="379.8" width="35.7" height="30.7"/>
            <rect x="69.1" y="318.7" width="35.7" height="30.7"/>
            <rect x="192.7" y="326.3" width="350.1" height="11.3"/>
            <rect x="192.7" y="389.1" width="350.1" height="11.3"/>
            <rect x="192.7" y="451.9" width="350.1" height="11.3"/>
            <rect x="192.7" y="514.6" width="350.1" height="11.3"/>
          </svg>
        </div>
      </div>
    </div>
    <div class="video-player" v-if="showPlayer">
      <iframe width="100%" height="500" src="https://www.youtube.com/embed/cYROqsUAw0o" frameborder="0"
              allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
      <img src="../assets/svg/close-youTube-player.svg" @click="closeVideo()" class="video-player-close">
    </div>
    <div class="wrapper-items" v-bind:class="{'wrapper-items--list': listView}">
      <div class="items"
           v-bind:style="{'margin-top': listView ? sliderPos + 'px' : 0, 'margin-left': !listView ? sliderPos + 'px' : 0}"
           @mousedown.prevent="onMouseDown($event)">
        <div class="item" v-for="(movie, index) of filteredData">
          <h5 class="item__heading-card">{{ movie.title }}</h5>
          <span class="item__year-card">{{ movie.year }}</span>
          <div class="poster">
            <img
              :src="movie.poster"
              alt="film-image" class="poster__logo">
            <img src="../assets/svg/movie-type.svg" class="poster__logo-left" alt="poster-icon">
            <img src="../assets/svg/products/actions/gradeless-white.svg" class="poster__logo-right" alt="poster-icon">
            <div class="poster__logo-center" @click="showVideo()"><img src="../assets/svg/play-button.svg"
                                                                       alt="poster-icon"></div>
          </div>
          <div class="rating">
            <svg width="75" height="75" viewBox="0 0 120 120">
              <circle cx="60" cy="60" r="50" fill="none" stroke="#d3f4e3" stroke-width="20"/>
              <circle cx="60" cy="60" r="50" fill="none" stroke="#22ca71" stroke-width="20" stroke-dasharray="314.16"
                      :stroke-dashoffset="314.16 * (1 - (movie.rank || movie.expectations_count) / 10)"/>
            </svg>
            <span class="rating__label">{{ movie.rank || movie.expectations_count }}</span>

          </div>
          <div class="item__info">
            <h5 class="item__info-heading">{{ movie.title }}</h5>
            <div class="item__info-wrapper">
              <span class="item__info-data">{{ movie.year }} | </span>
              <span class="item__info-data"> Director: {{ movie.director }} | </span>
              <span class="item__info-data"> Writer: {{ movie.writer }}</span>
            </div>
            <p class="item__info-desc">{{ movie.content }}</p>
            <div class="item__info-bottom">
              <div class="item__info-items">
                <div class="item__info-item">
                  <img src="../assets/svg/products/actions/share.svg" class="item__info-icon" alt="item-logo">
                </div>
                <div class="item__info-item">
                  <span class="item__info-num">{{ movie.comments_count }}<span class="item__info-line">|</span></span>
                  <img src="../assets/svg/products/actions/comment.svg" class="item__info-icon" alt="item-logo">
                </div>
                <div class="item__info-item">
                  <span class="item__info-num">{{ movie.expectations_count || movie.rank }}<span
                    class="item__info-line">|</span></span>
                  <img src="../assets/svg/products/actions/gradeless.svg" class="item__info-icon" alt="item-logo">
                </div>
                <div class="item__info-item">
                  <span class="item__info-num">{{ movie.likes_count }}<span class="item__info-line">|</span></span>
                  <img src="../assets/svg/products/actions/heart.svg" class="item__info-icon" alt="item-logo">
                </div>
              </div>
              <div class="item__info-link">
                <a :href="movie.link" target="_blank">Read more</a>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="slider">
        <button class="slider__button"><img src="../assets/svg/verticali-slider-arrows.svg" class="slider__button-top">
        </button>
        <button class="slider__button"><img src="../assets/svg/verticali-slider-arrows.svg"
                                            class="slider__button-bottom"></button>
      </div>
    </div>
  </section>
</template>

<script>
    export default {
        name: 'MoviesList',
        props: {
            title: String,
            movies: Array,
            initialListView: Boolean
        },
        data() {
            return {
                selectedFilter: String,
                filteredData: Array,
                listView: this.initialListView,
                down: false,
                dragStartPoint: Number,
                sliderPos: 0,
                cardItemWidth: 295,
                showPlayer: false
            }
        },
        created() {
            this.selectAll();
            if (process.client) {
                window.addEventListener('mouseup', () => this.onMouseUp());
                window.addEventListener('mousemove', (event) => this.drag(event));
            }
        },
        methods: {
            transformToCards() {
                this.listView = false;
                this.sliderPos = 0;
            },
            transformToList() {
                this.listView = true;
                this.sliderPos = 0;
            },
            selectAll() {
                this.filteredData = this.movies;
                this.sliderPos = 0;
                this.selectedFilter = 'All'
            },
            selectMovies() {
                this.sliderPos = 0;
                this.selectedFilter = 'Movie';
                this.filteredData = this.movies.filter(item => item.type === this.selectedFilter);
            },
            selectTvShows() {
                this.sliderPos = 0;
                this.selectedFilter = 'TV-Show';
                this.filteredData = this.movies.filter(item => item.type === this.selectedFilter);
            },
            drag(event) {
                if (!this.listView) {
                    const availableScrollWidth = this.cardItemWidth * this.filteredData.length - document.body.offsetWidth;
                    if (this.down) {
                        const draggedDistance = event.clientX - this.dragStartPoint;
                        if (draggedDistance > 0 || availableScrollWidth < 0) {
                            this.sliderPos = 0
                        } else if (draggedDistance < -availableScrollWidth) {
                            this.sliderPos = -availableScrollWidth
                        } else {
                            this.sliderPos = draggedDistance
                        }
                    }
                } else {
                    const availableScrollWidth = 240 * this.filteredData.length - 760;
                    if (this.down) {
                        const draggedDistance = event.clientY - this.dragStartPoint;
                        if (draggedDistance > 0 || availableScrollWidth < 0) {
                            this.sliderPos = 0
                        } else if (draggedDistance < -availableScrollWidth) {
                            this.sliderPos = -availableScrollWidth
                        } else {
                            this.sliderPos = draggedDistance
                        }
                    }
                }

            },
            onMouseDown(event) {
                this.down = true;
                this.dragStartPoint = this.listView ? event.clientY - this.sliderPos : event.clientX - this.sliderPos;
            },
            onMouseUp() {
                this.down = false
            },
            showVideo() {
                this.showPlayer = true
            },
            closeVideo() {
                this.showPlayer = false
            }

        }
    }
</script>

<style lang="scss">

  .rating {
    display: none;
  }

  .video-player {
    position: relative;
    .video-player-close {
      position: absolute;
      top: 20px;
      left: 50%;
      transform: translateX(-50%);
      width: 40px;
      cursor: pointer;
      transition: ease-out 0.3s;
    }

    .video-player-close:hover {
      transform: scale(1.4) translateX(-50%);
    }
  }

  .filter {
    background-color: black;
    height: 63px;
    padding: 11px 115px;
    margin-top: -4px;
    display: flex;
    justify-content: space-between;

    &__heading {
      font-size: 30px;
      color: #F5F5F5;
      font-family: 'Roboto-Condensed-Bold';
    }

    &__item {
      display: flex;
      justify-content: space-between;

    }

    &__button {
      width: 134px;
      height: 40px;
      padding: 9px auto;
      margin-left: 24px;
      background-color: black;
      border: 2px solid #F5F5F5;
      color: #F5F5F5;
      border-radius: 5px;
      font-size: 22px;
      cursor: pointer;
      outline: none;
      font-family: 'Roboto-Condensed-Bold';
    }

    &__button--active,
    &__button:hover {
      background-color: #F5F5F5;
      color: #000000;
    }

    &__icons {
      display: flex;
      margin-left: 50px;
      align-items: center;
    }

    &__icon:first-child {
      margin-right: 22px;
    }

    &__icon {
      width: 39px;
      height: 19px;
      fill: #4d5255;
      cursor: pointer;

    }

    &__icon--active,
    &__icon:hover {
      fill: #F5F5F5;
    }
  }

  .wrapper-items {
    width: 100%;
    height: auto;
  }

  .wrapper-items .slider {
    display: none;
  }

  .items {
    white-space: nowrap;
    overflow: hidden;
  }

  .item {
    display: inline-block;
    width: 220px;
    padding: 20px 0 15px;
    margin: 0 37.5px;

    &__heading-card,
    &__year-card {
      font-size: 20px;
      color: #000000;
      overflow: hidden;
      text-overflow: ellipsis;
      font-family: 'Roboto-Bold';
    }

    &__year-card {
      font-size: 15px;
    }

    &__info {
      width: 100%;
      display: flex;

      &-bottom {
        width: 100%;
      }

      &-items {
        display: flex;
      }

      &-heading,
      &-wrapper,
      &-desc,
      &-link {
        display: none;
      }


      &-item {
        width: 25%;
        display: flex;
        align-items: center;
        flex-direction: column;

      }

      &-icon {
        width: 21px;
        height: 21px;
      }

      &-icon:first-child {
        margin-top: 33px;
      }

      &-num {
        font-size: 12px;
        color: #000000;
        margin: 10px 0 12px;
        font-family: 'Proxima-Nova';
      }

      &-line {
        display: none;
      }

      &-btn {
        display: none;
      }
    }
  }

  .poster {
    height: 330px;
    width: 100%;
    position: relative;
    overflow: hidden;
    margin-top: 15px;

    &__logo {
      height: 100%;
      border-radius: 3px;

      &-left,
      &-center,
      &-right {
        position: absolute;
      }

      &-left {
        top: 7px;
        left: 10px;
        width: 37px;
      }

      &-right {
        top: 4px;
        right: 13px;
        width: 37px;
      }

      &-center {
        top: 50%;
        left: 50%;
        padding: 18px 14px 16px 21px;
        border-radius: 50%;
        background-color: rgba(8, 25, 37, 0.73);
        transform: translate(-50%, -50%);
        cursor: pointer;
        transition: ease-out 0.3s;

        img {
          width: 23px;
        }
      }
      &-center:hover {
        background-color: rgba(34, 108, 160, 0.81);
      }

    }
  }

  .slider {
    display: none;
  }

  .wrapper-items--list {
    margin: 0 115px;
    padding: 20px 0;
    display: flex;
    width: auto;
    height: 760px;
    overflow: hidden;

    .slider {
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      width: 25px;

      &__button {
        border: none;
        width: 25px;
        padding: 5px;
        cursor: pointer;
        outline: none;
        background: none;

        &:last-child {
          transform: rotate(180deg);
        }
      }
    }

    .items {
      white-space: normal;
      flex-grow: 1;

      .poster,
      .rating,
      .item__info {
        display: inline-block;
      }

      .rating {
        width: 105px;
        padding: 0 15px;
        margin-top: 40px;
        position: relative;
        vertical-align: top;
        color: #22ca71;

        &__label {
          font-size: 22px;
          position: absolute;
          left: 50%;
          top: 50%;
          transform: translate(-50%, -50%);
          font-family: 'Gotham-Bold';
        }

        svg {
          transform: rotate(-90deg);
        }
      }

      .poster {
        width: 106px;
        height: auto;
        vertical-align: top;
        margin-top: 0;

        &__logo {
          height: auto;
          width: 100%;

          &-left,
          &-right {
            display: none;
          }
        }
      }


      .item {
        margin: 20px 0;
        font-size: 0;
        width: 100%;

        &__heading-card,
        &__year-card {
          display: none;
        }

        &__info {
          width: calc(100% - 213px);

          &-link {
            display: block;

            a {
              font-size: 20px;
              color: #389ef2;
              font-family: 'Roboto-Condensed-Bold';
            }
          }

          &-heading {
            display: block;
            font-size: 16px;
            color: #389ef2;
            font-family: 'Roboto-Condensed-Bold';
          }

          &-wrapper {
            display: block;
          }

          &-data {
            display: inline-block;
            font-size: 18px;
            color: #000000;
            font-family: 'Roboto-Condensed-Bold';
          }

          &-desc {
            display: block;
            font-size: 18px;
            color: #4b555d;
            font-family: 'Roboto-Regular';
          }

          &-bottom {
            display: flex;
            justify-content: space-between;
            margin-top: 30px;
          }

          &-items {
            white-space: nowrap;
            display: flex;
          }

          &-item {
            display: inline-flex;
            width: 25%;
            font-size: 0;
            margin-left: 50px;
            align-items: center;
            flex-direction: row;
          }

          &-item:first-child {
            margin-left: 0;
          }

          &-icon {
            width: 25px;
            height: 25px;
          }

          &-icon:first-child {
            margin-top: 0;
          }

          &-num {
            font-size: 14px;
            vertical-align: center;
          }

          &-line {
            display: inline-block;
            margin: 0 10px;
          }

          &-btn button {
            font-size: 20px;
            color: #389ef2;
            outline: none;
            text-decoration: none;
            cursor: pointer;
            border: none;
            border-bottom: 1px solid #389ef2;

          }
        }
      }
    }
  }


</style>
