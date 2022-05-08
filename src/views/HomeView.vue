<template>
  <main>
    <div class="container py-4">
      <header class="pb-3 mb-4 border-bottom">
        <a
          href="/"
          class="d-flex align-items-center text-dark text-decoration-none"
        >
          <svg
            height="80px"
            style="enable-background: new 0 0 512 512"
            version="1.1"
            viewBox="0 0 512 512"
            width="80px"
            xml:space="preserve"
            xmlns="http://www.w3.org/2000/svg"
            xmlns:xlink="http://www.w3.org/1999/xlink"
          >
            <g id="_x33_67-vuejs">
              <g>
                <polygon
                  points="392.46,59.011 313.5,59.011 256.001,149.983 206.716,59.011 26.001,59.011     256.001,452.989 485.999,59.011   "
                  style="fill: #41b883"
                />
                <polygon
                  points="83.192,91.867 138.433,91.867 256.001,295.378 373.464,91.867 428.705,91.867     256.001,387.787 83.192,91.867   "
                  style="fill: #35495e"
                />
              </g>
            </g>
            <g id="Layer_1" />
          </svg>
          <span class="fs-4">Vue JS - QR Code Generator</span>
        </a>
      </header>

      <div class="p-5 mb-4 bg-light rounded-3">
        <div class="container-fluid py-3">
          <h1 class="display-5 fw-bold">Free generated QR codes</h1>
          <p class="col-md-8 fs-4">
            Codes QR générés gratuitement que vous pouvez utiliser pour vos
            besoins professionnels ou personnels.
          </p>
          <div class="my-3">
            <div class="input-group mb-3">
              <input
                v-model="QrValue"
                class="form-control form-control-lg"
                type="text"
                placeholder="Paste an url to create your first qr code..."
              />
              <button
                type="button"
                class="btn btn-dark"
                @click="downLoadQRcode"
              >
                Download
              </button>
            </div>
          </div>
          <div class="row">
            <div
              ref="qrcode"
              class="col-12 d-flex aligns-items-center justify-content-center mt-5"
            >
              <qrcode-vue
                v-if="QrValue"
                :value="QrValue"
                :size="250"
                level="H"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import QrcodeVue from "qrcode.vue";
import { ref } from "vue";
export default {
  name: "HomeView",
  components: {
    QrcodeVue,
  },
  setup() {
    const QrValue = ref(null);
    const qrcode = ref(null);

    const downLoadQRcode = () => {
      // console.log(QrValue.value);

      let canvasImage = qrcode.value
        .getElementsByTagName("canvas")[0]
        .toDataURL("image/png");
      let xhr = new XMLHttpRequest();
      xhr.responseType = "blob";
      xhr.onload = function () {
        let a = document.createElement("a");
        a.href = window.URL.createObjectURL(xhr.response);
        a.download = "qrcode.png";
        a.style.display = "none";
        document.body.appendChild(a);
        a.click();
        a.remove();
      };
      xhr.open("GET", canvasImage);
      xhr.send();
    };

    return {
      downLoadQRcode,
      QrValue,
      qrcode,
    };
  },
};
</script>

<style lang="css">
.bd-placeholder-img {
  font-size: 1.125rem;
  text-anchor: middle;
  -webkit-user-select: none;
  -moz-user-select: none;
  user-select: none;
}

@media (min-width: 768px) {
  .bd-placeholder-img-lg {
    font-size: 3.5rem;
  }
}
</style>
