<template >
  <div class="container-fluid mycontent">
    <div class="row justify-content-center h-100">
      <div class="col-md-4 col-xl-3 chat">
        <div class="card mb-sm-3 mb-md-0 contacts_card">
          <div class="card-header">
            <div class="input-group">
              <div class="input-group-prepend text-light">Envia tu mensaje</div>
            </div>
          </div>
          <div class="card-body contacts_body">
            <form class="row g-2 m-3 mt-0" v-on:submit.prevent="sendMessage">
              <div class="col">
                <img
                  width="150"
                  :src="require(`@/assets/img/${chat.avatar}`)"
                />
                <select
                  class="form-select"
                  id="validationCustom04"
                  v-model="chat.avatar"
                  required
                >
                  <option selected value="avatar1.png">Avatar 1</option>
                  <option value="avatar2.png">Avatar 2</option>
                  <option value="avatar3.png">Avatar 3</option>
                  <option value="avatar4.png">Avatar 4</option>
                </select>
                <div class="invalid-feedback">Please select a valid state.</div>
              </div>
              <div class="col-12">
                <label for="validationDefault01" class="form-label"
                  >Nombre</label
                >
                <input
                  type="text"
                  class="form-control"
                  id="transmitter"
                  name="transmitter"
                  placeholder="nombre...."
                  v-model="chat.transmitter"
                  required
                />
              </div>

              <div class="col-12">
                <label for="validationDefault01" class="form-label"
                  >Mensaje</label
                >

                <textarea
                  class="form-control"
                  aria-label="With textarea"
                  id="message"
                  name="message"
                  v-model="chat.message"
                  placeholder="escribe tu mensaje..."
                  required
                ></textarea>
              </div>

              <div class="col-12">
                <button class="btn btn-send" type="submit">Enviar</button>
              </div>
            </form>
          </div>
          <div class="card-footer"></div>
        </div>
      </div>
      <div class="col-md-8 col-xl-6 chat">
        <div class="card">
          <div class="card-header msg_head">
            <div class="d-flex bd-highlight">
              <div class="img_cont">
                <img src="../assets/logo.png" class="rounded-circle user_img" />
                <span class="online_icon"></span>
              </div>
              <div class="user_info">
                <span>Chat PORTH</span>
                <p>{{ countMessages }} mensajes</p>
              </div>
            </div>
          </div>
          <div class="card-body msg_card_body">
            <div v-if="countMessages > 0">
              <div v-for="(chat, index) in chats" :key="chat.id">
                <div
                  v-if="index % 2 != 0"
                  class="d-flex justify-content-start mb-5"
                >
                  <div class="img_cont_msg">
                    <img
                      :src="require(`@/assets/img/${chat.avatar}`)"
                      class="rounded-circle user_img_msg"
                    />
                  </div>
                  <div class="msg_cotainer">
                    <span class="msg_name">{{ chat.transmitter }}</span>
                    {{ chat.text_message }}
                    <span class="msg_time">{{ chat.date }}</span>
                  </div>
                </div>

                <div
                  v-else-if="index % 2 == 0"
                  class="d-flex justify-content-end mb-5"
                >
                  <div class="msg_cotainer_send">
                    <span class="msg_name">{{ chat.transmitter }}</span>
                    {{ chat.text_message }}
                    <span class="msg_time_send">{{ chat.date }}</span>
                  </div>
                  <div class="img_cont_msg">
                    <img
                      :src="require(`@/assets/img/${chat.avatar}`)"
                      class="rounded-circle user_img_msg"
                    />
                  </div>
                </div>
              </div>
            </div>
            <div v-else-if="countMessages < 1">
              <h3 class="text-light">NO EXISTEN MENSAJES AUN EN EL CHAT....</h3>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      chats: [],
      countMessages: "",
      chat: {
        avatar: "avatar1.png",
      },
    };
  },
  created: function () {
    this.getChats();
  },
  methods: {
    getChats() {
      fetch("http://localhost:4000/chat/")
        .then((res) => res.json())
        .then((dataResponse) => {
          this.chats = [];
          if (typeof dataResponse[0].success === "undefined") {
            this.chats = dataResponse;
            this.chats.forEach((element) => {
              element.date = new Date(element.date).toLocaleString();
            });

            this.countMessages = this.chats.length;
          }
        })
        .catch(console.log);
    },
    sendMessage() {
      var data = {
        transmitter: this.chat.transmitter,
        message: this.chat.message,
        date: new Date(),
        avatar: this.chat.avatar,
      };
      fetch("http://localhost:4000/chat/create/", {
        method: "POST",
        body: JSON.stringify(data),
        headers: {
          "Content-type": "application/json",
        },
      })
        .then((response) => response.json())
        .then(() => {
          window.location.href = "/chat";
        });
    },
  },
};
</script>

<style>
.mycontent {
  background-image: url(../assets/fondo.png);
  background-repeat: repeat;
}
.chat {
  margin-top: auto;
  margin-bottom: auto;
}
.card {
  height: 550px;
  border-radius: 15px !important;
  background-color: rgba(31, 62, 102, 0.4) !important;
}
.contacts_body {
  padding: 0.75rem 0 !important;
  overflow-y: auto;
  white-space: nowrap;
}
.msg_card_body {
  overflow-y: auto;
}
.card-header {
  border-radius: 15px 15px 0 0 !important;
  border-bottom: 0 !important;
}
.card-footer {
  border-radius: 0 0 15px 15px !important;
  border-top: 0 !important;
}
.container {
  align-content: center;
}
.search {
  border-radius: 15px 0 0 15px !important;
  background-color: rgba(0, 0, 0, 0.3) !important;
  border: 0 !important;
  color: white !important;
}
.search:focus {
  box-shadow: none !important;
  outline: 0px !important;
}
.type_msg {
  background-color: rgba(0, 0, 0, 0.3) !important;
  border: 0 !important;
  color: white !important;
  height: 60px !important;
  overflow-y: auto;
}
.type_msg:focus {
  box-shadow: none !important;
  outline: 0px !important;
}
.attach_btn {
  border-radius: 15px 0 0 15px !important;
  background-color: rgba(0, 0, 0, 0.3) !important;
  border: 0 !important;
  color: white !important;
  cursor: pointer;
}
.send_btn {
  border-radius: 0 15px 15px 0 !important;
  background-color: rgba(0, 0, 0, 0.3) !important;
  border: 0 !important;
  color: white !important;
  cursor: pointer;
}
.search_btn {
  border-radius: 0 15px 15px 0 !important;
  background-color: rgba(0, 0, 0, 0.3) !important;
  border: 0 !important;
  color: white !important;
  cursor: pointer;
}
.contacts {
  list-style: none;
  padding: 0;
}
.contacts li {
  width: 100% !important;
  padding: 5px 10px;
  margin-bottom: 15px !important;
}
.active {
  background-color: rgba(0, 0, 0, 0.3);
}
.user_img {
  height: 70px;
  width: 70px;
  border: 1.5px solid #f5f6fa;
}
.user_img_msg {
  height: 40px;
  width: 40px;
  border: 1.5px solid #f5f6fa;
}
.img_cont {
  position: relative;
  height: 70px;
  width: 70px;
}
.img_cont_msg {
  height: 40px;
  width: 40px;
}
.online_icon {
  position: absolute;
  height: 15px;
  width: 15px;
  background-color: #4cd137;
  border-radius: 50%;
  bottom: 0.2em;
  right: 0.4em;
  border: 1.5px solid white;
}
.offline {
  background-color: #c23616 !important;
}
.user_info {
  margin-top: auto;
  margin-bottom: auto;
  margin-left: 15px;
}
.user_info span {
  font-size: 20px;
  color: white;
}
.user_info p {
  font-size: 10px;
  color: rgba(255, 255, 255, 0.6);
}
.video_cam {
  margin-left: 50px;
  margin-top: 5px;
}
.video_cam span {
  color: white;
  font-size: 20px;
  cursor: pointer;
  margin-right: 20px;
}
.msg_cotainer {
  margin-top: auto;
  margin-bottom: auto;
  margin-left: 10px;
  border-radius: 25px;
  background-color: #82ccdd;
  padding: 10px;
  position: relative;
  min-width: 100px;
}
.msg_cotainer_send {
  margin-top: auto;
  margin-bottom: auto;
  margin-right: 10px;
  border-radius: 25px;
  background-color: #78e08f;
  padding: 10px;
  position: relative;
  min-width: 100px;
}
.msg_time {
  position: absolute;
  left: 0;
  bottom: -15px;
  color: rgba(255, 255, 255);
  font-size: 10px;
}
.msg_name {
  position: absolute;
  left: 10px;
  top: -18px;
  color: rgba(255, 255, 255);
  font-size: 10px;
}
.msg_time_send {
  position: absolute;
  right: 0;
  bottom: -15px;
  color: rgba(255, 255, 255);
  font-size: 10px;
}
.msg_head {
  position: relative;
}
#action_menu_btn {
  position: absolute;
  right: 10px;
  top: 10px;
  color: white;
  cursor: pointer;
  font-size: 20px;
}
.action_menu {
  z-index: 1;
  position: absolute;
  padding: 15px 0;
  background-color: rgba(0, 0, 0, 0.5);
  color: white;
  border-radius: 15px;
  top: 30px;
  right: 15px;
  display: none;
}
.action_menu ul {
  list-style: none;
  padding: 0;
  margin: 0;
}
.action_menu ul li {
  width: 100%;
  padding: 10px 15px;
  margin-bottom: 5px;
}
.action_menu ul li i {
  padding-right: 10px;
}
.action_menu ul li:hover {
  cursor: pointer;
  background-color: rgba(0, 0, 0, 0.2);
}
@media (max-width: 576px) {
  .contacts_card {
    margin-bottom: 15px !important;
  }
}
.btn-send {
  background-color: #82ccdd;
}
.btn-send:hover {
  background-color: #78e08f;
}
</style>