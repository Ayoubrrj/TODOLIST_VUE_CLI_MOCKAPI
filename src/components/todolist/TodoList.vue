<script setup>
import { reactive, onMounted } from "vue";
import DB from "@/services/DB";
import TodoListAddForm from "./TodoListAddForm.vue";
import TodoListFooter from "./TodoListFooter.vue";
import Todo from "./Todo.vue";

const todos = reactive([]);

onMounted(async () => {
    DB.setApiURL("https://68db8534445fdb39dc25a900.mockapi.io/");
    todos.splice(todos.length, 0, ...(await DB.findAll()));
    console.table(todos);
});
</script>
<template>
    <!-- CARD LISTE -->
    <section
        class="bg-slate-100 rounded-xl shadow ring-1 ring-slate-200/60 overflow-hidden"
        aria-labelledby="todo-heading"
    >
        <h2 id="todo-heading" class="sr-only">Todo list</h2>

        <!-- INPUT PRINCIPAL -->
        <TodoListAddForm />

        <!-- LISTE DES TODOS -->
        <ul
            class="m-4 divide-y divide-slate-200 text-slate-800"
            role="list"
            aria-label="Todos"
        >
            <!-- ITEM (exemple) <todo v-for="t in todos" :key="t.id" :turlututu="t" />-->
            <todo v-for="todo in todos" :key="todo.id" :todo="todo" />

            <!-- Message si aucun todo (à gérer en Vue) -->
            <li
                class="px-4 py-6 sm:px-5 text-slate-400 italic text-center hidden"
                role="listitem"
            >
                No tasks yet.
            </li>
        </ul>

        <!-- FOOTER DE LISTE -->
        <TodoListFooter />
    </section>
</template>
<style scoped></style>
