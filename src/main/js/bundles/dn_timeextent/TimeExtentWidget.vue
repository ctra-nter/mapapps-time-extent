<template xmlns:v-slot="http://www.w3.org/1999/XSL/Transform">
    <div>
        <v-select
            :items="layers"
            v-model="selectedLayerId"
            class="pa-0"
            item-value="id"
            item-text="title"
            single-line
            hide-details
        >
        </v-select>

        <v-layout row>
            <v-menu
                ref="startDateMenu"
                v-model="startDateMenuShow"
                :close-on-content-click="false"
                :return-value.sync="startDateVal"
                lazy
                transition="scale-transition"
                offset-y
                full-width
                min-width="290px"
            >
                <template v-slot:activator="{ on }">
                    <v-text-field
                        v-model="startDateVal"
                        label="Start Datum"
                        prepend-icon="event"
                        readonly
                        v-on="on"
                    ></v-text-field>
                </template>
                <v-date-picker v-model="startDateVal" no-title scrollable>
                    <v-spacer></v-spacer>
                    <v-btn flat color="primary" @click="startDateMenuShow = false">Cancel</v-btn>
                    <v-btn flat color="primary" @click="$refs.startDateMenu.save(startDateVal)">OK</v-btn>
                </v-date-picker>
            </v-menu>


            <v-menu
                ref="startTimeMenu"
                v-model="startTimeMenuShow"
                :close-on-content-click="false"
                :return-value.sync="startTimeVal"
                lazy
                transition="scale-transition"
                offset-y
                full-width
                max-width="290px"
                min-width="290px"
            >
                <template v-slot:activator="{ on }">
                    <v-text-field
                        v-model="startTimeVal"
                        label="Start Time"
                        prepend-icon="access_time"
                        readonly
                        v-on="on"
                    ></v-text-field>
                </template>
                <v-time-picker
                    v-if="startTimeMenuShow"
                    v-model="startTimeVal"
                    full-width
                    @click:minute="$refs.startTimeMenu.save(startTimeVal)"
                ></v-time-picker>
            </v-menu>
        </v-layout>

        <v-spacer></v-spacer>

        <v-layout row>
            <v-menu
                ref="endDateMenu"
                v-model="endDateMenuShow"
                :close-on-content-click="false"
                :return-value.sync="endDateVal"
                lazy
                transition="scale-transition"
                offset-y
                full-width
                min-width="290px"
            >
                <template v-slot:activator="{ on }">
                    <v-text-field
                        v-model="endDateVal"
                        label="End Datum"
                        prepend-icon="event"
                        readonly
                        v-on="on"
                    ></v-text-field>
                </template>
                <v-date-picker v-model="endDateVal" no-title scrollable>
                    <v-spacer></v-spacer>
                    <v-btn flat color="primary" @click="endDateMenuShow = false">Cancel</v-btn>
                    <v-btn flat color="primary" @click="$refs.endDateMenu.save(endDateVal)">OK</v-btn>
                </v-date-picker>
            </v-menu>


            <v-menu
                ref="endTimeMenu"
                v-model="endTimeMenuShow"
                :close-on-content-click="false"
                :return-value.sync="endTimeVal"
                lazy
                transition="scale-transition"
                offset-y
                full-width
                max-width="290px"
                min-width="290px"
            >
                <template v-slot:activator="{ on }">
                    <v-text-field
                        v-model="endTimeVal"
                        label="End Time"
                        prepend-icon="access_time"
                        readonly
                        v-on="on"
                    ></v-text-field>
                </template>
                <v-time-picker
                    v-if="endTimeMenuShow"
                    v-model="endTimeVal"
                    full-width
                    @click:minute="$refs.endTimeMenu.save(endTimeVal)"
                ></v-time-picker>
            </v-menu>
        </v-layout>

        <v-spacer></v-spacer>

        <v-btn
            block
            ripple
            color="primary"
            @click="$emit('setFilter', {})">
            {{ i18n.filter }}
        </v-btn>
    </div>
</template>

<script>
    import Bindable from "apprt-vue/mixins/Bindable";

    export default {
        components: {},
        mixins: [Bindable],
        props: {
            i18n: {
                type: Object,
                default: function () {
                    return {
                        filter: "Filter"
                    }
                }
            },
            layers: {
                type: Array,
                default: function(){
                    return []
                }
            },
            selectedLayerId: {
                type: String,
                default: ""
            },
            startDateVal: {
                type: Date,
                default: new Date().toISOString().substr(0, 10)
            },
            startDateMenuShow: {
              type: Boolean,
              default: false
            },
            startTimeMenuShow: {
                type: Boolean,
                default: false
            },
            startTimeVal: {
                default: null
            },
            endDateVal: {
                type: Date,
                default: new Date().toISOString().substr(0, 10)
            },
            endDateMenuShow: {
                type: Boolean,
                default: false
            },
            endTimeMenuShow: {
                type: Boolean,
                default: false
            },
            endTimeVal: {
                default: null
            }
        }
    };
</script>
