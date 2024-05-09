<template>
    <div class="title">
        <h1>Notification <span v-if="unreadMessages > 0">{{ unreadMessages }}</span></h1>
        <span @click="handleMarkAllRead">Mark all as read</span>
    </div>
    <ul class="notifications" v-for="user in users" :key="user.id">
        <Notifier :user="user" @openMessage="handleOpenMessage"/>
    </ul>
</template>

<script setup>
import { ref, computed } from 'vue';
import Notifier from './Notifier.vue';

const users = ref([
    {
        id: 3,
        username: 'Mark Webber',
        avator: '/images/avatar-mark-webber.webp',
        message: 'reacted to your recent post',
        post: 'My first tournament today!',
        duration: '1m ago',
        read: false
    },
    {
        id: 1,
        avator: "/images/avatar-angela-gray.webp",
        username: 'Angela Gray',
        message: 'followed you',
        duration: '5m ago',
        read: false,
    },
    {
        id: 4,
        username: 'Jacob Thompson',
        message: 'has joined your group',
        avator: "/images/avatar-jacob-thompson.webp",
        group:'Chess Club',
        duration: '1 day ago',
        read: false,
    },
    {
        id: 5,
        username: 'Rizky Hasanuddin',
        message: 'sent you a private message',
        privateMessage: 'Hello, thanks for setting up the Chess Club. I\'ve been member for a few weeks now and I\'m already having lots of fun and improving my game.',
        duration: '5 days ago',
        read: true,
        avator: '/images/avatar-rizky-hasanuddin.webp',
    },
    {
        id: 6,
        username: 'Kimberly Smith',
        avator: '/images/avatar-kimberly-smith.webp',
        duration: '1 week ago',
        read: true,
        message: 'commented on your picture',
        postImage: '/images/image-chess.webp',
    },
    {
        id: 7,
        username: 'Nathan Peterson',
        avator: '/images/avatar-nathan-peterson.webp',
        message: 'reacted to your recent post  your ',
        post: '5 end-game strategies to increase win rate',
        duration: '2 week ago',
        read: true

    },
    {
        id: 2,
        avator: "/images/avatar-anna-kim.webp",
        username: 'Anna Kim',
        message: 'left the group',
        group:'Chess Club',
        duration: '2 week ago',
        read: true,
    }
]);

const unreadMessages = computed(() => {
    return users.value.reduce((acc, current) => {
        return !current.read ? acc += 1 : acc
    }, 0)
});

const handleMarkAllRead = () => {
    users.value = users.value.map(user => {
        return !user.read ? {...user, read:true} : user
    });
}

const handleOpenMessage = (id) => {
    users.value = users.value.map((u) => {
        if (id === u.id) {
            return { ...u, read: true };
        } else {
            return { ...u }
        }
    });
}
</script>

<style scoped>

.notifications {
    list-style-type: none;
    transition: all 0.54s ease;
}

.title {
    display: flex;
    place-items: center;
    place-content: space-between;
    font-size: .6rem;
    transition: all 0.54s ease;
}

.title h1 {
    font-family: 'PlusJakartaSans-ExtraBold';
}

.title h1 > span {
    background-color: var(--blue);
    padding: 0rem .6rem;
    color: var(--white);
    border-radius: .4rem;
}

.title > span {
    font-family: 'PlusJakartaSans-Medium';
    color: var(--blue);
    cursor: pointer;
    font-size: .9rem;
}

@media screen and (min-width:768px) {

    .title {
        font-size: 1rem;
    }
    .title h1 > span {
        align-self: flex-end;
        font-size: 1.3rem;
    }
}

@media screen  and (min-width:1024px) {
    .title {
        font-size: 1.4rem;
    }

    .title h1 > span {
        font-size: 1.7rem;
    }
}
</style>
