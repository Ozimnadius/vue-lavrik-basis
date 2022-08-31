<template>
  <div id="calc">
    <div class="container">
      <h2>Калькулятор тортика</h2>
      <hr>
      <button type="button"
              class="btn btn-primary"
              v-on:click="addLayer">
        Добавить слой
      </button>
      <hr>
      <div class="row">
        <div class="col-6">
          <div class="layers">
            <div class="layer"
                 v-bind:class="`layer-${layer.type}`"
                 v-bind:style="{height: layer.height*10+'px'}"
                 v-for="(layer,i) in layers"
                 v-on:click="addHeight(i)"
                 v-on:contextmenu.prevent="removeHeight(i)">
              {{ layer.type }}
            </div>
          </div>
        </div>
        <div class="col-6">
          <table class="table table-bordered">
            <thead>
            <tr>
              <th>Тип</th>
              <th>Высота</th>
              <th>Удалить</th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="(layer,i) in layers">
              <td>
                <select class="form-select"
                        v-model="layer.type">
                  <option v-bind:value="typeKey"
                          v-for="(type, typeKey) in layersTypes">
                    {{ type.label }}
                  </option>
                </select>
              </td>
              <td>
                <input class="form-control"
                       type="number"
                       name="height"
                       v-model="layer.height"
                >
              </td>
              <td>
                <button type="button"
                        class="btn btn-danger"
                        v-on:click="deleteLayer(i)">-
                </button>
              </td>
            </tr>
            </tbody>
          </table>
        </div>
      </div>
      <hr>
      <div class="alert alert-success">
        <span class="price"> {{ sum }} руб</span>
        <button type="button"
                class="btn btn-warning"
                v-b-modal.modal-1>
          Заказать
        </button>

        <b-modal id="modal-1" title="Итого">
          <p class="my-4">Вы заказали торт стоимостью {{sum}}</p>
        </b-modal>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'calc',
  data() {
    return {
      layers: [],
      layersTypes: {
        biscuit: {
          price1cm: 50,
          label: 'Бисквит'
        },
        beze: {
          price1cm: 100,
          label: 'Безе'
        },
        curd: {
          price1cm: 60,
          label: 'Творожный'
        }
      },
      defaultType: 'biscuit',
      defaultHeigth: 4,
    }
  },
  computed: {
    sum() {
      return this.layers.reduce((sum, i) => {
        return sum + this.layersTypes[i.type].price1cm * i.height;
      }, 0)
    }
  },
  methods: {
    addLayer() {
      this.layers.push({
        type: this.defaultType,
        height: this.defaultHeigth
      });
    },
    deleteLayer(i) {
      this.layers.splice(i, 1);
    },
    addHeight(i) {
      this.layers[i].height += 1;
    },
    removeHeight(i) {
      this.layers[i].height -= 1;
    }
  }
}
</script>

<style scoped>
#calc {
  padding: 100px 0;
}

.layer-biscuit {
  background: #fee4c3;
}

.layer-beze {
  background: #d8b8ba;
}

.layer-curd {
  background: #bca483;
}

</style>
