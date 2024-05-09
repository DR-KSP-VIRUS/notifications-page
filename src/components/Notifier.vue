<template>
    <li :class="user.read ? 'notification' :'notification unread' " @click="onOpenMessage(user.id)">
        <picture class="avator">
            <img :src="user.avator" :alt="user.username+' avator'">
        </picture>
        <div class="notification-message">
            <div class="user-post">
                <p>{{ user.username }}
                    <span class="message">{{ user.message }} 
                        <span class="post">{{ user.post }}</span> 
                        <span class="group">{{ user.group }}</span>
                    </span>
                    <span :class="!user.read ? 'new-message':''" v-if="!user.   read"></span>
                </p>
                <img class="post-image" v-if="user.postImage" :src="user.postImage"/>
            </div>
            <div class="time-stamp">{{ user.duration }}</div>
        </div>
    </li>
    <div class="private-message" v-if="user.privateMessage">
        <p>{{ user.privateMessage }}</p>
    </div>
</template>

<script setup>
const emit = defineEmits(['openMessage']);

const props = defineProps({
    user: {
        type: Object,
        required: true,
    },
});

const onOpenMessage = (id) => {
    emit("openMessage", id);
}
</script>

<style scoped>
.notification {
    display: flex;
    place-items: center;
    margin: 1rem 0;
    padding: .5rem 1rem;
    font-family: 'PlusJakartaSans-Medium';
    border-radius: .44rem;
    transition: all 0.54s ease;
}
.unread {
    background-color: var(--light-grayish-blue-1);
    cursor: pointer;
}
.avator {
    margin-right: 1rem;
}

.avator img {
    height: 3rem;
}

.notification-message {
    display: flex;
    flex-direction: column;
    transition: all 0.54s ease;
}

.user-post {
    display: grid;
    grid-template-columns: 10fr 1fr;
    align-items: center;
    font-family: 'PlusJakartaSans-ExtraBold';
}

.post-image {
    height: 4rem;
    width: 4rem;
    margin-left: 1rem;
}


.time-stamp {
    color: var(--grayish-blue);
}

.message {
    color: var(--grayish-blue);
    position: relative;
}

.post {
    color: var(--dark-grayish-blue);
}

.unread .post {
    color: var(--dark-grayish-blue);
    font-family: 'PlusJakartaSans-ExtraBold';
}

.group {
    color: var(--blue);
    font-family: 'PlusJakartaSans-ExtraBold';
}

.private-message {
    margin: 0 .5rem 0 4.5rem;
    padding: 1rem 1.5rem;
    font-family: 'PlusJakartaSans-Medium';
    border: 1.2px solid var(--grayish-blue);
    border-radius: 0.4rem;
    outline: 2px;
    font-size: 1.3rem;
}
.new-message {
    width: 10px;
    height: 10px;
    border-radius: 50%;
    background-color: var(--red);
    position: absolute;
    margin:0.4rem;
}

@media screen and (min-width:1024px) {
    .notification-message {
        font-size: 1.2rem;
    }
}
</style>
