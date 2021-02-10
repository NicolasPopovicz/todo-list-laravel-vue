<template>
    <div class="addItem">
        <input type="text" v-model="item.name" />
        <font-awesome-icon
            icon="plus-square"
            @click="addItem()"
            :class="[item.name ? 'active' : 'inactive', 'plus']"
        />
    </div>
</template>

<script>
export default {
    data: function () {
        return {
            item: {
                name: "",
            },
        };
    },
    methods: {
        addItem() {
            if (this.item.name === "") {
                return;
            }

            axios
                .post("api/item/store", {
                    item: this.item,
                })
                .then((response) => {
                    if (response.status === 201) {
                        this.item.name = "";
                        this.$emit("reloadlist");
                    }
                })
                .catch((e) => {
                    console.log(e);
                });
        },
    },
};
</script>

<style scoped>
.addItem {
    display: flex;
    justify-content: center;
    align-items: center;
}

input {
    background: #f7f7f7;
    border: none;
    outline: none;
    padding: 5px;
    margin-right: 10px;
    width: 100%;
    font-family: Nunito;
}

.plus {
    font-size: 20px;
    transition: 0.3s;
    cursor: pointer;
}

.plus:hover {
    transform: scale(0.9);
}

.active {
    color: #00ce25;
}

.inactive {
    color: #999999;
}
</style>
