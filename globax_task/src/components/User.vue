<template>
    <div class="dialog-card">
        <div class="user_cards">
            <div class="card" style="width: 28rem; height: 28rem">
                <div class="card-body" v-for="user in users">
                    <div class="card_title">
                      <h5 class="card-title">{{ user.name }}</h5>
                      <img src="@/assets/icon.svg" alt=""  @click="isVisible">
                    </div>
                    
                    <div class="contact">
                        <div class="title">
                            <p class="paragraph"><span>Телефон:</span></p>
                            <p class="paragraph"><span>Почта:</span></p>
                            <p class="paragraph"><span>Дата приема:</span></p>
                            <p class="paragraph"><span>Должность:</span></p>
                            <p class="paragraph"><span>Подразделение:</span></p>
                        </div>
                        <div class="title">
                            <p class="paragraph">
                                <span>{{ user.phone }}</span>
                            </p>
                            <p class="paragraph">
                                <span>{{ user.email }}</span>
                            </p>
                            <p class="paragraph">
                                <span>{{ user.hire_date }}</span>
                            </p>
                            <p class="paragraph">
                                <span>{{ user.position_name }}</span>
                            </p>
                            <p class="paragraph">
                                <span>{{ user.departament }}</span>
                            </p>
                        </div>
                    </div>
                    <div class="dop">
                        <p class="card-text">
                            Дополнительная информация:
                            <span>{{ user.address }}</span>
                        </p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ["users", 'isVisible'],
    
};
</script>

<style scoped>
.card_title {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
}
.card {
    border: none;
}
</style>
