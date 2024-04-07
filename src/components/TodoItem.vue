<template>
    <el-col :span="12" >
        <el-card class="issue-card" shadow="hover">
            <el-row :gutter="12">
                <el-col :span="18">
                    {{ todo }}
                </el-col>
                <el-col :span="4">
                    <el-button
                        icon="el-icon-check"
                        circle
                        type="success"
                        @click="completeTodo()"
                    ></el-button>
                </el-col>
            </el-row>
        </el-card>
    </el-col>
</template>

<script>
export default {
    name: "TodoItem",

    props: {
        todo: String,
        index: Number,
    },
    methods: {
        completeTodo() {
            this.$emit('close-todo', this.index);
        }
    }
};
</script>