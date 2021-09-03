<template>
    <div>
        <span>Итого можете внести в качестве досрочных:</span>
        <Checkbox
            v-for="deduction in deductions"
            :key = "deduction.id"
            :deduction='deduction'
        />
    </div>
</template>

<script>
    import Checkbox from '@/components/Checkbox.vue'

    export default {
        name: 'Calc',
        props: {
            deductions: {
                type: Array,
            }
        },
        components: {
            Checkbox
        }
}
</script>

<style scoped>
 span{
    display: block;
    font-weight: 500;
    font-size: 14px;
    line-height: 24px;
    margin-right: 32px;
    margin-top: 12px;
  }
</style>
