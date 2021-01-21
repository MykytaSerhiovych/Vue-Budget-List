<template>
    <el-card class="form-card">
        <el-form :model="formData" ref="addItemForm" :rules="rules" label-position="top">
            <el-form-item label="Type" prop="type">
                <el-select class="type-select" v-model="formData.type" placeholder="Choose type...">
                    <el-option label="Income" value="INCOME"/>
                    <el-option label="Outcome" value="OUTCOME"/>
                </el-select>
            </el-form-item>
            <el-form-item label="Comments" prop="comment">
                <el-input v-model="formData.comment"/>
            </el-form-item>
             <el-form-item label="Value" prop="value">
                <el-input v-model.number="formData.value"/>
            </el-form-item>
            <el-button @click="onSubmit" type="primary">Submit</el-button>
        </el-form>
    </el-card>
</template>

<script>
export default {
    name: "Form",
    data: () => ({
        formData: {
            type: 'INCOME',
            comment: "",
            value: 0
        },
        rules: {
            type: [
                {required : true, message: "Please select type", trigger: "blur"}
            ],
            comment: [
                {required : true, message: "Please input comment type", trigger: "change"}
            ],
            value: [
                {required : true, message: "Please input value", trigger: "change"},
                {type: 'number', message: "Value must be a number", trigger: "change"},
                {validator: (rule, value, callback) => {
                    if(value != 0){
                        callback();
                    } else {
                        callback('Zero is not acceptable!');
                    }
                }, trigger: "blur"}
            ]
        }
    }),
    methods: {
        onSubmit() {
            this.$refs.addItemForm.validate((valid) => {
               if(valid) {
                   const typeData = {...this.formData};
                   this.checkTypeData(typeData);
                   this.$emit('submitForm', {...this.formData});
                   this.$refs.addItemForm.resetFields();
               }
            });
        },
        checkTypeData(typeData) {
            if(typeData.type === 'INCOME') {
                typeData.value = Math.abs(typeData.value);
            }
            if(typeData.type === 'OUTCOME') {
                typeData.value = -Math.abs(typeData.value);
            }
        }
    }
};
</script>

<style scoped>
.form-card {
    max-width: 500px;
    margin: auto;
    text-align: left;
}
.type-select {
    width: 100%;
}
</style>
