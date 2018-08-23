<template>
    <div>
        <div class="WYSIWYG" ref="WYSIWYG"
             contenteditable="true"
             @focus="handleFocus"
             @input="emitChange"
             v-html="content"></div>
        <h1>{{txt}}</h1>
        <button @click="txt = new Date()">Update Child</button>
    </div>
</template>

<script>
    import 'at.js';
    import 'at.js/dist/css/jquery.atwho.min.css';
    import $ from 'jquery';

    // TODO check https://teratail.com/questions/86786

    export default {
        name: "WYSIWYG",
        props: {
            value: {
                type: String,
                default: ''
            },
            disabled: {
                type: Boolean,
                default: false
            }
        },
        data() {
            return {
                txt: 'BBBBB',
                content: this.value,
                customTagOptions: [
                    {
                        at: "@",
                        data: [
                            {label: 'Jacob', value: 'Jacob@email.com'},
                            {label: 'Isabella', value: 'Isabella@email.com'},
                            {label: 'Ethan', value: 'Ethan@email.com'},
                            {label: 'Emma', value: 'Emma@email.com'},
                            {label: 'Michael', value: 'Michael@email.com'},
                            {label: 'Olivia', value: 'Olivia@email.com'},
                            {label: 'Alexander', value: 'Alexander@email.com'},
                            {label: 'Sophia', value: 'Sophia@email.com'},
                            {label: 'William', value: 'William@email.com'},
                            {label: 'Ava', value: 'Ava@email.com'},
                            {label: 'Joshua', value: 'Joshua@email.com'},
                            {label: 'Emily', value: 'Emily@email.com'},
                            {label: 'Daniel', value: 'Daniel@email.com'},
                            {label: 'Madison', value: 'Madison@email.com'},
                            {label: 'Jayden', value: 'Jayden@email.com'},
                            {label: 'Abigail', value: 'Abigail@email.com'},
                            {label: 'Noah', value: 'Noah@email.com'},
                            {label: 'Chloe', value: 'Chloe@email.com'},
                            {label: '你好', value: '你好@email.com'},
                            {label: '你你你', value: '你你你@email.com'},
                            {label: 'Jérémy', value: 'Jérémy@email.com'}
                        ],
                        startWithSpace: false,
                        searchKey: 'label',
                        headerTpl: '<div class="atwho-header">Member List</div>',
                        displayTpl: '<li>${label}</li>',
                        insertTpl: '<span class="WYSIWYG__CustomTag" data-value="${value}">@${label}</span>',
                        limit: 10000
                    }
                ]
            };
        },
        beforeCreate() {
            // eslint-disable-next-line
            console.log('[==> C ]beforeCreate');
        },
        created() {
            // eslint-disable-next-line
            console.log('[==> C ]created');
        },
        beforeMount() {
            // eslint-disable-next-line
            console.log('[==> C ]beforeMount');
        },
        mounted() {
            // eslint-disable-next-line
            console.log('[==> C ]mounted');
            const $el = $(this.$refs['WYSIWYG']);

            this.customTagOptions.forEach(opt => {
                if (!opt['callbacks']) opt['callbacks'] = {};
                opt['callbacks']['beforeInsert'] = (value) => {
                    setTimeout(() => {
                        this.emitChange();
                    }, 300);
                    return value;
                };

                $el.atwho(opt);
            });
        },
        beforeUpdate() {
            // eslint-disable-next-line
            console.log('[==> C ]beforeUpdate');
        },
        updated() {
            // eslint-disable-next-line
            console.log('[==> C ]updated');
        },
        beforeDestroy() {
            // eslint-disable-next-line
            console.log('[==> C ]beforeDestroy');
        },
        destroyed() {
            // eslint-disable-next-line
            console.log('[==> C ]destroyed');
        },
        methods: {
            emitChange() {
                const $el = $(this.$refs['WYSIWYG']);
                // eslint-disable-next-line
                console.log('[==> C ]emitChange');
                this.$emit('input', $el.html());
            },
            handleFocus(evt) {
                if (evt && this.disabled) evt.currentTarget.blur();
            }
        }
    };
</script>

<style>
    .atwho-view {
        z-index: 10000 !important
    }

    .atwho-view .cur {
        color: var(--color-white);
        background: var(--color-green);
    }

    .atwho-header {
        display: flex;
        justify-content: space-between;
    }

    .atwho-inserted .WYSIWYG__CustomTag {
        color: var(--color-white);
        background: var(--color-green);
        padding: 4px;
        border-radius: 4px;
    }
</style>

<style scoped>
    .WYSIWYG {
        -moz-appearance: none;
        -webkit-appearance: none;
        border-radius: 2px;
        background-color: var(--color-white);
        border: solid 1px;
        padding: 9px 8px;
        font-size: 12px;
        color: var(--color-black);
        text-align: left;
        resize: none;
        height: auto;
    }

    .WYSIWYG:focus {
        outline: 0;
        border: solid 1px var(--color-green);
    }

    .WYSIWYG__CustomTag {
        background: var(--color-gray);
        color: var(--color-white);
        padding: 4px;
        border-radius: 4px;
    }
</style>
