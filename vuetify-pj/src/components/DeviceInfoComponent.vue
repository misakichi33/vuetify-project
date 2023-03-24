<script lang="ts" setup>
import { ref, withDefaults } from "vue";
const show1 = ref(false);
const show2 = ref(false);
// const show3 =ref(false);

withDefaults(
    defineProps<{
      deviceInfo:
        | {
            asNumber: string
            rd: string
            importPolicy?: string
            exportPolicy?: string
            interface: {
              name: string
              description: string
              ipAddress: {
                address: string
                isSecondary: boolean
              }[]
            }[]
            bgpNeighbor: {
              address: string
              as: string
            }[]
          }
        | null
    }>(),
    {
      deviceInfo: null,
    }
  )

  </script>

<template>
  <v-card
    class="mx-auto"
    style="width: 500px"
  >
    <!-- General Infomation start -->
    <v-card-title> General Infomation </v-card-title>

    <v-table fixed-header style="padding-left: 16px; padding-right: 16px">
      <tbody>
        <tr>
          <td>AS Number</td>
          <td>{{ deviceInfo?.asNumber }}</td>
        </tr>
        <v-divider style="border-top-width: 0px"></v-divider>

        <tr>
          <td>RD</td>
          <td>{{ deviceInfo?.rd }}</td>
        </tr>
        <v-divider style="border-top-width: 0px"></v-divider>

        <tr>
          <td>Import Policy</td>
          <td v-if="deviceInfo?.importPolicy">{{ deviceInfo?.importPolicy }}</td>
          <td v-else>-</td>
        </tr>
        <v-divider style="border-top-width: 0px"></v-divider>

        <tr>
          <td>Export Policy</td>
          <td v-if="deviceInfo?.exportPolicy">{{ deviceInfo?.exportPolicy }}</td>
          <td v-else>-</td>
        </tr>
      </tbody>
    </v-table>
    <!-- General Infomation end -->

    <!-- Interface start -->
    <v-card-actions style="padding: 0px">
      <v-card-title> Interface </v-card-title>
      <v-spacer></v-spacer>

      <v-btn
        :icon="show1 ? 'mdi-chevron-up' : 'mdi-chevron-down'"
        @click="show1 = !show1"
      >
      </v-btn>
    </v-card-actions>

    <v-card elevation="0" style="padding-left: 16px; padding-right: 16px">
      <div v-show="show1">
        <div v-for="(inter, interIndex) in deviceInfo?.interface" :key="interIndex">
          <v-card-title> {{ inter.name }} </v-card-title>

          <v-table fixed-header style="padding-left: 16px; padding-right: 16px">
            <tbody>
              <tr>
                <td>Description</td>
                <td>{{ inter.description }}</td>
              </tr>
              <v-divider style="border-top-width: 0px"></v-divider>
              <tr>
                <td>IP Address</td>
                <td>
                  <div v-for="(ipAddress, ipAddressIndex) in inter.ipAddress" :key="ipAddressIndex">
                    {{ ipAddress.address }}
                    <span v-if="ipAddress.isSecondary"> secondary </span>
                  </div>
                </td>
              </tr>
            </tbody>
          </v-table>
        </div>
      </div>
    </v-card>
    <!-- Interface end -->

    <!-- Routing start -->
    <v-card-actions style="padding: 0px">
      <v-card-title> Routing </v-card-title>

      <v-spacer></v-spacer>

      <v-btn
        :icon="show2 ? 'mdi-chevron-up' : 'mdi-chevron-down'"
        @click="show2 = !show2"
      >
      </v-btn>
    </v-card-actions>

    <div v-show="show2">
      <v-table fixed-header style="padding-left: 16px; padding-right: 16px">
        <tbody>
          <tr>
            <td>{{ deviceInfo?.exportPolicy }}</td>
            <td>{{ deviceInfo?.exportPolicy }}</td>
          </tr>
        </tbody>
      </v-table>
    </div>
    <!-- Routing end -->

    <!-- SR Policy start -->
    <!-- <v-card-actions style="padding: 0px;">
        <v-card-title>
        SR Policy
        </v-card-title>
        <v-spacer></v-spacer>

        <v-btn
        :icon="show3 ? 'mdi-chevron-up' : 'mdi-chevron-down'"
        @click="show3 = !show3"
        >
        </v-btn>
    </v-card-actions>

        <div v-show="show3">
            <v-table
            fixed-header
            style="padding-left: 16px; padding-right: 16px;"
            >
            <tbody>
                <tr>
                    <td>SR</td>
                    <td>{{ deviceInfo?.srPolicy }}</td>
                </tr>
                <v-divider style="border-top-width: 0px;"></v-divider>

                <tr>
                    <td>IP Address</td>
                    <td>{{ deviceInfo?.interface }}</td>
                </tr>
            </tbody>
            </v-table>
        </div> -->
    <!-- SR Policy end -->
  </v-card>
</template>
