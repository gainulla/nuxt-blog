<template>
  <div v-if="articles" class="articles">
    <article v-for="(article, i) in articles" :key="i">
      <div class="article-inner">
        <div class="row">
          
          <div class="column col-md-5 col-lg-4">
            <nuxt-link :to="article.path">
              <img :src="require(`~/assets/images/featured/${article.image}`)" />
            </nuxt-link>
          </div>

          <div class="column">
            <div class="details">
              <h2 class="title">
                <nuxt-link :to="article.path">{{ article.title }}</nuxt-link>
              </h2>
              <p class="description">
                {{ article.description }}<nuxt-link :to="article.path">...</nuxt-link>
              </p>
              <div class="tags">
                <nuxt-link
                  v-for="(tag, i) of $tagsArr(article.allLanguages)"
                  :to="pathFor('/blog/tag', $i18n.locale, tag)"
                  :key="i"
                >{{ $tagsArr(article.allLanguages).length > (i + 1)
                  ? `${tag},` : tag }}
                </nuxt-link>
              </div>
            </div>
          </div>

        </div>
      </div>
    </article>
  </div>

  <div v-else class="articles">
    <h3 class="text-center mt-2">No posts yet.</h3>
  </div>
</template>

<script>
export default {
  name: 'ArticlesList',

  props: ['articles'],
}
</script>

<style lang="scss" scoped>
.articles {
  padding-bottom: 2rem;

  article {
    background-color: white;
    border-radius: .4rem;
    margin-bottom: .5rem;
    font-size: 1.2rem;

    .article-inner {
      img {
        display: block;
        width: 100%;
        height: 100%;
        max-height: 300px;
        margin: 0 1.5rem 0 0;
        object-fit: cover;
        cursor: pointer;
      }

      .details {
        text-align: left;

        .title {
          margin: 0;
          font-family: var(--secondary-font);
          cursor: pointer;
        }

        .description {
          font-family: var(--secondary-font);
        }

        .tags {
          align-self: flex-end;
        }
      }
    }
  }
}

@media (min-width: 576px) {
  .articles {
    padding-left: 1rem;
    padding-right: 1rem;

    article {
      .article-inner {
        img {
          min-height: 320px;
          max-height: 320px;
        }
      }
    }
  }
}

@media (min-width: 768px) {
  .articles {
    article {
      margin-bottom: 2rem;

      .article-inner {
        img {
          border-top-left-radius: .4rem;
          border-bottom-left-radius: .4rem;
          min-height: 250px;
          max-height: 250px;
        }
        .details {
          padding: 25px;
          height: 100%;
          border: 1px solid #EEE;
          border-top-right-radius: .4rem;
          border-bottom-right-radius: .4rem;
        }
      }
    }
  }
}
</style>