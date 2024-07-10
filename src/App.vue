<template>
    <div class="px-10 bg-slate-100 text-center">
        <ul class="grid grid-cols-5 gap-2 py-2 px-10 border-b-[2px]">
            <li
                v-for="(title, index) in data.header"
                :key="index"
                class="font-semibold"
            >
                {{ title }}
            </li>
        </ul>
        <ul
            class="border-b-[2px] grid grid-cols-5 px-10 py-2 text-center"
            v-for="(title, index) in data.body"
        >
            <li class="grid-cols-2 grid text-start">
                <button
                    class="bg-blue-400 w-7 rounded-md text-white"
                    @click="getToggleId(title.id)"
                >
                    {{ toggleId.includes(title.id) ? "-" : "+" }}
                </button>
                {{ title.id }}
            </li>
            <li>
                {{ title.name }}
            </li>
            <li>
                {{ title.username }}
            </li>
            <li>
                {{ title.age }}
            </li>
            <li>
                {{ title.city }}
            </li>
            <ul
                class="bg-slate-200 col-span-5 grid grid-cols-5 mt-2 py-2 font-semibold"
                :class="toggleId.includes(title.id) ? '' : 'hidden'"
            >
                <li>{{ title.decsription.d_header.id }}</li>
                <li>{{ title.decsription.d_header.costumer }}</li>
                <li>{{ title.decsription.d_header.status }}</li>
                <li>{{ title.decsription.d_header.date }}</li>
                <li>{{ title.decsription.d_header.amount }}</li>
            </ul>
            <div class="col-span-5 grid grid-cols-5 py-2">
                <ul
                    class="bg-slate-200 col-span-5 grid grid-cols-5 py-2 font-semibold"
                    :class="toggleId.includes(title.id) ? '' : 'hidden'"
                    v-for="(item, index) in title.decsription.d_body"
                >
                    <li>{{ item.id }}</li>
                    <li>{{ item.costumer }}</li>
                    <li :class="checkStatus(item.status).className">
                        {{ checkStatus(item.status).text }}
                    </li>
                    <li>{{ formatDate(item.date, false) }}</li>
                    <li>{{ item.amount }}</li>
                </ul>
            </div>
        </ul>
    </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
const toggleId = ref<Array<number>>([]);
const data = ref({
    header: {
        id: " actions / id",
        name: "name",
        username: "username",
        age: "age",
        city: "city",
    },
    body: [
        {
            id: 1,
            name: "john",
            username: "doe",
            age: 17,
            city: "new york",
            decsription: {
                d_header: {
                    id: "id",
                    costumer: "costumer",
                    status: "status",
                    date: "date",
                    amount: "amount",
                },
                d_body: [
                    {
                        id: 1001,
                        costumer: "mikel",
                        status: 1,
                        date: "10-01-2024",
                        amount: 100,
                    },
                    {
                        id: 1002,
                        costumer: "jeck",
                        status: 0,
                        date: "10-05-2023",
                        amount: 150,
                    },
                    {
                        id: 1003,
                        costumer: "tomson",
                        status: 0,
                        date: "10-10-2023",
                        amount: 140,
                    },
                ],
            },
        },
        {
            id: 2,
            name: "tony",
            username: "ben",
            age: 19,
            city: "los angelis",
            decsription: {
                d_header: {
                    id: "id",
                    costumer: "costumer",
                    status: "status",
                    date: "date",
                    amount: "amount",
                },
                d_body: [
                    {
                        id: 2001,
                        costumer: "ismen",
                        status: 1,
                        date: "09-01-2024",
                        amount: 100,
                    },
                    {
                        id: 2002,
                        costumer: "honse",
                        status: 0,
                        date: "05-05-2023",
                        amount: 170,
                    },
                    {
                        id: 2003,
                        costumer: "rows",
                        status: 1,
                        date: "10-10-2023",
                        amount: 190,
                    },
                ],
            },
        },
    ],
});

const checkStatus = (status_name: number) => {
    if (status_name === 0)
        return { text: "bajarilgan", className: "text-blue-500" };
    else return { text: "bajarilmagan", className: "text-red-500" };
};
const formatDate = (dateString: string, getHour = true) => {
    const date = new Date(dateString);

    const day = String(date.getDate()).padStart(2, "0");
    const month = String(date.getMonth() + 1).padStart(2, "0"); // Months are 0-based in JavaScript
    const year = date.getFullYear();
    const hours = String(date.getHours()).padStart(2, "0");
    const minutes = String(date.getMinutes()).padStart(2, "0");

    return getHour
        ? `${day}.${month}.${year} ${hours}:${minutes}`
        : `${day}.${month}.${year}`;
};

const getToggleId = function (id: number) {
    if (!toggleId.value.find((c: number) => c === id)) toggleId.value.push(id);
    else toggleId.value = toggleId.value.filter((p: number) => p !== id);
};
</script>

<style>
li {
    list-style: none;
}
</style>
