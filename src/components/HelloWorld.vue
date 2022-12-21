<template>
  <main>
    <section class="h">
      <div class=".wrap">
        <div class="search">
          <input
            type="text"
            class="searchTerm"
            v-model="url"
            placeholder="Enter Your Url"
          />
          <button type="submit" class="searchButton" @click="shrink">
            SHRINK
          </button>
        </div>
        <div v-show="token">
          <h1 class="txtcolor">{{ msg }}</h1>
          <a class="txtcolor" v-bind:href="shrink_url" target="_blank">{{
            shrink_url
          }}</a>
        </div>
      </div>
    </section>
    <section>
      <div class="title">
        <h1>LINK SHRINK!</h1>
        <p>
          Lorem ipsum dolor sit amet, consectetur adipisicing elit. Debitis
          expedita a modi quam, neque est officiis voluptas cupiditate
          reiciendis fugit eos minima voluptatum? Itaque enim illo, adipisci
          porro exercitationem voluptatum?
        </p>
      </div>
    </section>
    <section>
      <div class="cards">
        <div class="card">
          <div class="content">
            <div class="front">
              <img src="../assets/facebook.png" alt="" />
            </div>
            <div class="back">
              <a href="facebook.com">Facebook</a>
            </div>
          </div>
        </div>
        <div class="card">
          <div class="content">
            <div class="front">
              <img src="../assets/facebook-messenger.png" alt="" />
            </div>
            <div class="back">
              <a href="facebook.com">Messenger</a>
            </div>
          </div>
        </div>
        <div class="card">
          <div class="content">
            <div class="front">
              <img src="../assets/twitter.png" alt="" />
            </div>
            <div class="back">
              <a href="twitter.com">Twitter</a>
            </div>
          </div>
        </div>
        <div class="card">
          <div class="content">
            <div class="front">
              <img src="../assets/gmail.png" alt="" />
            </div>
            <div class="back">
              <a href="gmail.com">Gmail</a>
            </div>
          </div>
        </div>
      </div>
    </section>
  </main>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      url: "",
      msg: "Shrinked Url",
      shrink_url: "",
      token: false,
    };
  },
  methods: {
    shrink() {
      this.token = true;
      const url = new URL("https://t.ly/api/v1/link/shorten");

      const params = {
        api_token:
          "XoXgo4GaLbsxzMY0PqNMkqAytzcZIpiaR0uJFDdATZwQfC5dTyfJJs76UMEJ",
      };
      Object.keys(params).forEach((key) =>
        url.searchParams.append(key, params[key])
      );

      const headers = {
        "Content-Type": "application/json",
        Accept: "application/json",
      };
      let body = {
        long_url: this.url,
        domain: "https://t.ly/",
        include_qr_code: false,
      };

      fetch(url, {
        method: "POST",
        headers,
        body: JSON.stringify(body),
      })
        .then((response) => response.json())
        .then((data) => {
          console.log(data.short_url);
          this.shrink_url = data.short_url;
        });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.search {
  width: fit-content;
  position: relative;
  display: flex;
}
.txtcolor {
  color: #b6b6bd;
}

.searchTerm {
  width: 450px;
  border: 3px solid #b6b6bd;
  border-right: none;
  padding: 5px;
  height: 20px;
  border-radius: 5px 0 0 5px;
  outline: none;
  color: #0a0a0a;
}

.searchTerm:focus {
  color: #0d0d1e;
}

.searchButton {
  width: fit-content;
  height: 36px;
  border: 1px solid #b6b6bd;
  background: #b6b6bd;
  text-align: center;
  color: #fff;
  border-radius: 0 5px 5px 0;
  cursor: pointer;
  font-size: 20px;
}

/*Resize the wrap to see the search bar change!*/
.wrap {
  width: 100%;
}
.h {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 200px;
  background: #03446a;
  border-radius: 0 0 10% 10%;
  box-shadow: rgba(0, 0, 0, 0.45) 0px 25px 20px -20px;
}
.iconh {
  display: block;
}
.cards {
  display: flex;
  justify-content: space-around;
  align-items: center;
}
.card {
  margin-top: 50px;
  width: 200px;
  height: 200px;
  float: left;
  perspective: 500px;
}

.content {
  position: absolute;
  width: 100%;
  height: 100%;
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
  transition: transform 1s;
  transform-style: preserve-3d;
}

.card:hover .content {
  transform: rotateY(180deg);
  transition: transform 0.5s;
}

.front,
.back {
  position: absolute;
  height: 100%;
  width: 100%;
  background: white;
  line-height: 300px;
  text-decoration: none;
  text-align: center;
  font-size: 20px;
  border-radius: 5px;
  backface-visibility: hidden;
  display:flex;
  align-items: center;
  justify-content: center;
}
.back a{
  text-decoration: none;
  color: #beccd4;
}
.back {
  background: #03446a;
  color: white;
  transform: rotateY(180deg);
}
</style>
