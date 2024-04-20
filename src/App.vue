<template>
  <div id="app">
    <nav
      class="bg-white dark:bg-gray-900 fixed w-full z-20 top-0 start-0 border-b border-gray-200 dark:border-gray-600"
    >
      <div
        class="max-w-screen-xl flex flex-wrap items-center justify-between mx-auto p-4"
      >
        <div class="flex space-x-3 md:space-x-0">
          <span
            class="self-center text-2xl font-semibold whitespace-nowrap dark:text-white"
            >Epoch Timer</span
          >
        </div>

        <a href="#" class="flex items-center space-x-3">
          <img
            style="height: 60px"
            src="@/assets/logo.png"
            class="h-8"
            alt="DHS Logo"
          />
        </a>
      </div>
    </nav>

    <div style="margin-top: 90px" class="grid justify-items-center">
      <div
        class="absolute inset-x-0 -top-40 -z-10 transform-gpu overflow-hidden blur-3xl sm:-top-80"
        aria-hidden="true"
      >
        <div
          class="relative left-[calc(50%-11rem)] aspect-[1155/678] w-[36.125rem] -translate-x-1/2 rotate-[30deg] bg-gradient-to-tr from-[#ff80b5] to-[#9089fc] opacity-30 sm:left-[calc(50%-30rem)] sm:w-[72.1875rem]"
          style="
            clip-path: polygon(
              74.1% 44.1%,
              100% 61.6%,
              97.5% 26.9%,
              85.5% 0.1%,
              80.7% 2%,
              72.5% 32.5%,
              60.2% 62.4%,
              52.4% 68.1%,
              47.5% 58.3%,
              45.2% 34.5%,
              27.5% 76.7%,
              0.1% 64.9%,
              17.9% 100%,
              27.6% 76.8%,
              76.1% 97.7%,
              74.1% 44.1%
            );
          "
        ></div>
      </div>

      <div style="width: 1300px" class="p-5">
        <div>
          <div class="bg-netral-300 px-6 lg:px-8">
            <div class="grid grid-cols-2 gap-4 p-4">
              <div>
                <p class="ml-1">The Current Epoch Unix Timestamp</p>
                <div class="mt-4">
                  <label
                    for="price"
                    class="block text-sm font-medium leading-6 text-gray-900 ml-1"
                    >Enter a Timestamp</label
                  >
                  <div class="relative mt-2 rounded-md shadow-sm">
                    <input
                      v-model="inp.timestamp"
                      type="text"
                      class="block w-full rounded-md border-0 py-1.5 pl-7 pr-20 text-gray-900 ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                      placeholder="0.00"
                    />
                    <div class="absolute inset-y-0 right-0 flex items-center">
                      <label for="currency" class="sr-only">Currency</label>
                      <select
                        id="currency"
                        name="currency"
                        class="h-full rounded-md border-0 bg-transparent py-0 pl-2 pr-7 text-gray-500 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm"
                      >
                        <option>USD</option>
                        <option>CAD</option>
                        <option>EUR</option>
                      </select>
                    </div>
                  </div>
                  <p class="font-light text-sm font-sans ml-1">
                    Supports Unix timestamps in seconds, milliseconds,
                    microseconds and nanoseconds.
                  </p>
                </div>
                <div class="mt-3">
                  <button
                  @click="convertTimestamp()"
                    type="button"
                    class="text-white bg-gradient-to-r from-blue-500 via-blue-600 to-blue-700 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-blue-300 dark:focus:ring-blue-800 shadow-lg shadow-blue-500/50 dark:shadow-lg dark:shadow-blue-800/80 font-medium rounded-lg text-sm px-5 py-2.5 text-center me-2 mb-2"
                  >
                    Convert
                  </button>
                </div>
              </div>
              <div class="grid justify-items-center items-center">
                <div>
                  <p class="text-7xl">{{ String(now.unix_ts).split('.')[0] }}</p>
                  <div class="ml-4">
                    <p class="mt-3">Seconds since Jan 01 1970. (UTC)</p>
                    <p class="font-bold">{{ now.time }}</p>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <div class="grid  gap-4 p-4">
            <div class="col-span-3 ml-7">
              <div class="relative overflow-x-auto shadow-md sm:rounded-lg">
                <table
                  class="w-full text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400"
                >
                  <tbody>

                    <tr class="border-b border-gray-200 dark:border-gray-700">
                      <th
                        scope="row"
                        class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap bg-gray-50 dark:text-white dark:bg-gray-800"
                      >
                        GMT
                      </th>
                      <td
                        class="text-2xl px-6 py-4 text-black font-medium whitespace-nowrap"
                      >
                        {{ now.gmt }}
                      </td>
                    </tr>
                    <tr class="border-b border-gray-200 dark:border-gray-700">
                      <th
                        scope="row"
                        class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap bg-gray-50 dark:text-white dark:bg-gray-800"
                      >
                        Your Time Zone
                      </th>
                      <td
                        class="text-2xl px-6 py-4 text-black font-medium whitespace-nowrap"
                      >
                        {{ now.date }}
                      </td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </div>

            <div></div>
          </div>
        </div>

        <div>
          <div class="p-4">
            <div class="ml-7 col-span-3">
              <div class="flex">
                <div inline-datepicker 
                :data-date="tdy.date"
                id="inp_date"></div>

                <div class="grid justify-items-center items-center">
                  <div>
                    <div class="flex ml-5">
                      <div class="relative flex items-center max-w-[8rem] mx-2">
                        <button
                          type="button"
                          @click="dec('hrs')"
                          class="bg-gray-100 dark:bg-gray-700 dark:hover:bg-gray-600 dark:border-gray-600 hover:bg-gray-200 border border-gray-300 rounded-s-lg p-3 h-11 focus:ring-gray-100 dark:focus:ring-gray-700 focus:ring-2 focus:outline-none"
                        >
                          <svg
                            class="w-3 h-3 text-gray-900 dark:text-white"
                            aria-hidden="true"
                            xmlns="http://www.w3.org/2000/svg"
                            fill="none"
                            viewBox="0 0 18 2"
                          >
                            <path
                              stroke="currentColor"
                              stroke-linecap="round"
                              stroke-linejoin="round"
                              stroke-width="2"
                              d="M1 1h16"
                            />
                          </svg>
                        </button>
                        <input
                          type="text"
                          v-model="time.hrs"
                          data-input-counter
                          aria-describedby="helper-text-explanation"
                          class="bg-gray-50 border-x-0 border-gray-300 h-11 text-center text-gray-900 text-sm focus:ring-blue-500 focus:border-blue-500 block w-full py-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                          placeholder="00"
                          required
                        />
                        <button
                          type="button"
                          @click="inc('hrs')"
                          data-input-counter-increment="hours"
                          class="bg-gray-100 dark:bg-gray-700 dark:hover:bg-gray-600 dark:border-gray-600 hover:bg-gray-200 border border-gray-300 rounded-e-lg p-3 h-11 focus:ring-gray-100 dark:focus:ring-gray-700 focus:ring-2 focus:outline-none"
                        >
                          <svg
                            class="w-3 h-3 text-gray-900 dark:text-white"
                            aria-hidden="true"
                            xmlns="http://www.w3.org/2000/svg"
                            fill="none"
                            viewBox="0 0 18 18"
                          >
                            <path
                              stroke="currentColor"
                              stroke-linecap="round"
                              stroke-linejoin="round"
                              stroke-width="2"
                              d="M9 1v16M1 9h16"
                            />
                          </svg>
                        </button>
                      </div>

                      <div class="relative flex items-center max-w-[8rem] mx-2">
                        <button
                          type="button"
                          @click="dec('min')"
                          class="bg-gray-100 dark:bg-gray-700 dark:hover:bg-gray-600 dark:border-gray-600 hover:bg-gray-200 border border-gray-300 rounded-s-lg p-3 h-11 focus:ring-gray-100 dark:focus:ring-gray-700 focus:ring-2 focus:outline-none"
                        >
                          <svg
                            class="w-3 h-3 text-gray-900 dark:text-white"
                            aria-hidden="true"
                            xmlns="http://www.w3.org/2000/svg"
                            fill="none"
                            viewBox="0 0 18 2"
                          >
                            <path
                              stroke="currentColor"
                              stroke-linecap="round"
                              stroke-linejoin="round"
                              stroke-width="2"
                              d="M1 1h16"
                            />
                          </svg>
                        </button>
                        <input
                          type="text"
                          
                          v-model="time.min"
                          data-input-counter
                          aria-describedby="helper-text-explanation"
                          class="bg-gray-50 border-x-0 border-gray-300 h-11 text-center text-gray-900 text-sm focus:ring-blue-500 focus:border-blue-500 block w-full py-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                          placeholder="00"
                          required
                        />
                        <button
                          type="button"
                          @click="inc('min')"
                          data-input-counter-increment="minutes"
                          class="bg-gray-100 dark:bg-gray-700 dark:hover:bg-gray-600 dark:border-gray-600 hover:bg-gray-200 border border-gray-300 rounded-e-lg p-3 h-11 focus:ring-gray-100 dark:focus:ring-gray-700 focus:ring-2 focus:outline-none"
                        >
                          <svg
                            class="w-3 h-3 text-gray-900 dark:text-white"
                            aria-hidden="true"
                            xmlns="http://www.w3.org/2000/svg"
                            fill="none"
                            viewBox="0 0 18 18"
                          >
                            <path
                              stroke="currentColor"
                              stroke-linecap="round"
                              stroke-linejoin="round"
                              stroke-width="2"
                              d="M9 1v16M1 9h16"
                            />
                          </svg>
                        </button>
                      </div>

                      <div class="relative flex items-center max-w-[8rem] mx-2">
                        <button
                          type="button"
                          @click="dec('sec')"
                          class="bg-gray-100 dark:bg-gray-700 dark:hover:bg-gray-600 dark:border-gray-600 hover:bg-gray-200 border border-gray-300 rounded-s-lg p-3 h-11 focus:ring-gray-100 dark:focus:ring-gray-700 focus:ring-2 focus:outline-none"
                        >
                          <svg
                            class="w-3 h-3 text-gray-900 dark:text-white"
                            aria-hidden="true"
                            xmlns="http://www.w3.org/2000/svg"
                            fill="none"
                            viewBox="0 0 18 2"
                          >
                            <path
                              stroke="currentColor"
                              stroke-linecap="round"
                              stroke-linejoin="round"
                              stroke-width="2"
                              d="M1 1h16"
                            />
                          </svg>
                        </button>
                        <input
                          type="text"
                          
                          v-model="time.sec"
                          data-input-counter
                          aria-describedby="helper-text-explanation"
                          class="bg-gray-50 border-x-0 border-gray-300 h-11 text-center text-gray-900 text-sm focus:ring-blue-500 focus:border-blue-500 block w-full py-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                          placeholder="00"
                          required
                        />
                        <button
                          type="button"
                          @click="inc('sec')"
                          class="bg-gray-100 dark:bg-gray-700 dark:hover:bg-gray-600 dark:border-gray-600 hover:bg-gray-200 border border-gray-300 rounded-e-lg p-3 h-11 focus:ring-gray-100 dark:focus:ring-gray-700 focus:ring-2 focus:outline-none"
                        >
                          <svg
                            class="w-3 h-3 text-gray-900 dark:text-white"
                            aria-hidden="true"
                            xmlns="http://www.w3.org/2000/svg"
                            fill="none"
                            viewBox="0 0 18 18"
                          >
                            <path
                              stroke="currentColor"
                              stroke-linecap="round"
                              stroke-linejoin="round"
                              stroke-width="2"
                              d="M9 1v16M1 9h16"
                            />
                          </svg>
                        </button>
                      </div>

                      <div class="relative flex items-center max-w-[8rem] mx-2">
                        <div class="ml-6 mt-1">
                          <button
                          @click="getInpDate()"
                            type="button"
                            class="text-white bg-gradient-to-r from-blue-500 via-blue-600 to-blue-700 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-blue-300 dark:focus:ring-blue-800 shadow-lg shadow-blue-500/50 dark:shadow-lg dark:shadow-blue-800/80 font-medium rounded-lg text-sm px-5 py-2.5 text-center me-2 mb-2"
                          >
                            Convert
                          </button>
                        </div>
                      </div>
                    </div>

                    <div class="ml-8 mt-4">
                      <table
                    class="w-full text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400"
                  >
                    <tbody>
                      <tr class="border-b border-gray-200 dark:border-gray-700">
                        <th
                          scope="row"
                          class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap bg-gray-50 dark:text-white dark:bg-gray-800"
                        >
                          Unix Timestamp
                        </th>
                        <td
                          class="text-2xl px-6 py-4 text-black font-medium whitespace-nowrap"
                        >
                          {{ report_2.unts }}
                        </td>
                      </tr>
                      <tr class="border-b border-gray-200 dark:border-gray-700">
                        <th
                          scope="row"
                          class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap bg-gray-50 dark:text-white dark:bg-gray-800"
                        >
                          GMT
                        </th>
                        <td
                          class="text-2xl px-6 py-4 text-black font-medium whitespace-nowrap"
                        >
                         {{ report_2.gmt }}
                        </td>
                      </tr>
                      <tr class="border-b border-gray-200 dark:border-gray-700">
                        <th
                          scope="row"
                          class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap bg-gray-50 dark:text-white dark:bg-gray-800"
                        >
                          Your Time Zone
                        </th>
                        <td
                          class="text-2xl px-6 py-4 text-black font-medium whitespace-nowrap"
                        >
                          {{ report_2.tz }}
                        </td>
                      </tr>
                     
                    </tbody>
                  </table>
                     
                    </div>

                    <p class="ml-8 mt-7">
                      <span class="font-bold"
                        >What is the unix time stamp?</span   
                      >
                      <br />
                      The unix time stamp is a way to track time as a running
                      total of seconds. This count starts at the Unix Epoch on
                      January 1st, 1970 at UTC. Therefore, the unix time stamp
                      is merely the number of seconds between a particular date
                      and the Unix Epoch. It should also be pointed out (thanks
                      to the comments from visitors to this site) that this
                      point in time technically does not change no matter where
                      you are located on the globe. This is very useful to
                      computer systems for tracking and sorting dated
                      information in dynamic and distributed applications both
                      online and client side.
                    </p>
                  </div>
                </div>
              </div>

              <div class="mt-7">
                <div class="relative overflow-x-auto shadow-md sm:rounded-lg">
                  
                </div>
              </div>
            </div>
            <div class="mx-9">
              <p class="mt-7">
                <span class="font-bold">What happens on January 19, 2038?</span
                ><br />
                On this date the Unix Time Stamp will cease to work due to a
                32-bit overflow. Before this moment millions of applications will
                need to either adopt a new convention for time stamps or be
                migrated to 64-bit systems which will buy the time stamp a "bit"
                more time.
              </p>

              <div class="mt-7">

            <div
            class="block p-6 bg-white border border-gray-200 rounded-lg shadow dark:bg-gray-800 dark:border-gray-700 ">
              
            <label for="countries" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Select an language to view code sinpets.</label>

            <select 
            v-model="lang"
            id="countries" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
              <option 
              v-for="(i,iv) in langs"
              :key="iv"
              >{{ i }}</option>
              
            </select>

              <p class="font-normal text-gray-700 dark:text-gray-400">
                <prism :language="language" :code="code[lang]">
                </prism>
              </p>
            </div>
  
                
              </div>

            </div>
            
          </div>
        </div>

        
        
      </div>

      <div
        class="absolute inset-x-0 top-[calc(100%-13rem)] -z-10 transform-gpu overflow-hidden blur-3xl sm:top-[calc(100%-30rem)]"
        aria-hidden="true"
      >
        <div
          class="relative left-[calc(50%+3rem)] aspect-[1155/678] w-[36.125rem] -translate-x-1/2 bg-gradient-to-tr from-[#ff80b5] to-[#9089fc] opacity-30 sm:left-[calc(50%+36rem)] sm:w-[72.1875rem]"
          style="
            clip-path: polygon(
              74.1% 44.1%,
              100% 61.6%,
              97.5% 26.9%,
              85.5% 0.1%,
              80.7% 2%,
              72.5% 32.5%,
              60.2% 62.4%,
              52.4% 68.1%,
              47.5% 58.3%,
              45.2% 34.5%,
              27.5% 76.7%,
              0.1% 64.9%,
              17.9% 100%,
              27.6% 76.8%,
              76.1% 97.7%,
              74.1% 44.1%
            );
          "
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
const moment = require('moment');
const timestamp = require('unix-timestamp');
import Prism from 'vue-prismjs'
import '@/vs-prism.css'

export default {
  name: "App",
  components: {
    Prism
  },
  data(){
    return{
      ids : {
        report_1 : ''
      },
      lang : 'Python',
      langs : [
        'Python','Sql','Javascript','Java','CSharp','C','CPP',
      ],
      report_2 : {
        unts : '-----------',
        gmt : '-----------',
        tz : '-----------',
        rel : '-----------'
      },
      inp : {
        timestamp : '',
        date : ''
      },
      now : {
        unix_ts : '',
        time : '',
        date : '',
        gmt : ''
      },
      time : {
        hrs : 0,
        min : 0,
        sec : 0
      },
      tdy :{
        date : '',
        stmp : ''
      }
    }
  },
  computed:{
    language(){
      return this.lang.toLowerCase()
    },
    code(){
      let code = {
                  Python : `
import datetime

# Unix timestamp
unix_timestamp =  ${this.tdy.stmp} # Example timestamp

# Convert Unix timestamp to datetime object
datetime_object = datetime.datetime.fromtimestamp(unix_timestamp)

# Format the datetime object as a string
formatted_date = datetime_object.strftime('%Y-%m-%d %H:%M:%S')

print(formatted_date)  # Output the formatted date string
                          `,

                          Sql : `
-- MySql
SELECT FROM_UNIXTIME(${this.tdy.stmp}) AS formatted_date;
SELECT DATE_FORMAT(FROM_UNIXTIME(${this.tdy.stmp}), '%Y-%m-%d %H:%i:%s') AS formatted_date;

-- PostgreSQL
SELECT TO_TIMESTAMP(${this.tdy.stmp}) AS formatted_date;
SELECT TO_TIMESTAMP(${this.tdy.stmp})::timestamp AS formatted_date;

-- BigQuery
SELECT DATETIME(TIMESTAMP_MILLIS(CAST(${this.tdy.stmp} AS INT64 ))) AS formatted_date;

-- Oracle
SELECT TO_CHAR(TO_TIMESTAMP(${this.tdy.stmp}), 'YYYY-MM-DD HH24:MI:SS') AS formatted_date FROM dual;

-- Sql Server
SELECT DATEDIFF(s, '1970-01-01 00:00:00', ${this.tdy.stmp} )

-- Teradata
SELECT FORMAT(CAST((${this.tdy.stmp} * 1000000) AS TIMESTAMP(0)), 'YYYY-MM-DD HH:MI:SS') AS formatted_date;

-- SQLite
SELECT datetime(${this.tdy.stmp} , 'unixepoch') AS formatted_date;

                          `,
                          Javascript : `\
// Unix timestamp (in milliseconds)
const unixTimestamp = ${this.tdy.stmp}; // Example timestamp

// Create a new Date object using the Unix timestamp
const dateObject = new Date(unixTimestamp);

// Extract date components
const year = dateObject.getFullYear();
const month = dateObject.getMonth() + 1; // Months are zero-based
const day = dateObject.getDate();
const hours = dateObject.getHours();
const minutes = dateObject.getMinutes();
const seconds = dateObject.getSeconds();

// Construct the date string
const dateString = \`\${year}-\${month.toString().padStart(2, '0')}-\${day.toString().padStart(2, '0')} \${hours.toString().padStart(2, '0')}:\${minutes.toString().padStart(2, '0')}:\${seconds.toString().padStart(2, '0')}\`;

console.log(dateString); // Output the formatted date string
                          `,
                          Java : `
import java.util.Date;

public class Main {
    public static void main(String[] args) {
        // Unix timestamp (in seconds)
        long unixTimestamp = ${this.tdy.stmp}; // Example timestamp

        // Convert Unix timestamp to milliseconds
        long milliseconds = unixTimestamp * 1000;

        // Create a new Date object using the milliseconds
        Date dateObject = new Date(milliseconds);

        // Output the formatted date string
        System.out.println(dateObject);
    }
}
                          `,
                          'CSharp' : `
using System;

class Program
{
    static void Main()
    {
        // Unix timestamp (in seconds)
        long unixTimestamp = ${this.tdy.stmp}; // Example timestamp

        // Convert Unix timestamp to DateTimeOffset
        DateTimeOffset dateTimeOffset = DateTimeOffset.FromUnixTimeSeconds(unixTimestamp);

        // Output the formatted date string
        Console.WriteLine(dateTimeOffset.ToString("yyyy-MM-dd HH:mm:ss"));
    }
}
                          `,
                          C : `
#include <stdio.h>
#include <time.h>

int main() {
    // Unix timestamp (in seconds)
    time_t unixTimestamp = ${this.tdy.stmp}; // Example timestamp

    // Convert Unix timestamp to struct tm
    struct tm *timeinfo;
    timeinfo = gmtime(&unixTimestamp); // or localtime(&unixTimestamp) for local time

    // Format the date string
    char dateString[20]; // Enough space for the formatted date string
    strftime(dateString, sizeof(dateString), "%Y-%m-%d %H:%M:%S", timeinfo);

    // Output the formatted date string
    printf("%s\n", dateString);

    return 0;
}
                          `,
                          CPP : `
#include <iostream>
#include <ctime>

int main() {
    // Unix timestamp (in seconds)
    time_t unixTimestamp = ${this.tdy.stmp}; // Example timestamp

    // Convert Unix timestamp to struct tm
    struct tm *timeinfo;
    timeinfo = std::gmtime(&unixTimestamp); // or std::localtime(&unixTimestamp) for local time

    // Format the date string
    char dateString[20]; // Enough space for the formatted date string
    strftime(dateString, sizeof(dateString), "%Y-%m-%d %H:%M:%S", timeinfo);

    // Output the formatted date string
    std::cout << dateString << std::endl;

    return 0;
}
                          
`
                        }

            return code

    }
  },
  methods:{
    convertTimestamp(){

      if(this.inp.timestamp != ''){
        clearInterval(this.ids.report_1)
        this.now.date = moment.unix(String(this.inp.timestamp))._d
        this.now.gmt = new Date(this.now.date).toUTCString()
        this.tdy.stmp = this.inp.timestamp 
      }
    },
    getInpDate(iopt = {
      is_load : false
    }){

      if(iopt.is_load){
        
        let date = new Date()

        let unixTimestamp = moment(date).unix()
        this.report_2.unts = unixTimestamp

        let gmt = new Date(date).toUTCString()
        this.report_2.gmt = gmt 

        this.report_2.tz = date
      }else{
        let inp_date = document.getElementById('inp_date')
        this.inp.date = inp_date.datepicker.getDate()

        let st = String(this.inp.date).split('00:00:00')[0]
        let time = `${st} ${this.time.hrs.toString().padStart(2, '0')}:${this.time.min.toString().padStart(2, '0')}:${this.time.sec.toString().padStart(2, '0')} `
        let date = new Date(time)

        let unixTimestamp = moment(date).unix()
        this.report_2.unts = unixTimestamp

        let gmt = new Date(date).toUTCString()
        this.report_2.gmt = gmt 

        this.report_2.tz = date
      }

    },
    inc(val){
      if(val == 'hrs' && Number(this.time.hrs) < 23){
        this.time.hrs = Number(this.time.hrs) + 1
      }
      if(val == 'min' && Number(this.time.min) < 59){
        this.time.min = Number(this.time.min) + 1
      }
      if(val == 'sec' && Number(this.time.sec) < 59){
        this.time.sec = Number(this.time.sec) + 1
      }
    },
    dec(val){
      if(val == 'hrs' && Number(this.time.hrs) > 0){
        this.time.hrs = Number(this.time.hrs) - 1
      }
      if(val == 'min' && Number(this.time.min) > 0){
        this.time.min = this.time.min - 1
      }
      if(val == 'sec' && this.time.sec > 0){
        this.time.sec = this.time.sec - 1
      }
    }
  },
  mounted(){
  
    let today = new Date();
    let month = String(today.getMonth() + 1).padStart(2, '0'); // Add 1 because months are zero-based
    let day = String(today.getDate()).padStart(2, '0');
    let year = today.getFullYear();

    let formattedDate = `${month}/${day}/${year}`;
    this.tdy.date = formattedDate
    this.inp.date = String(today).split(" ").slice(0, 4).join(" ")

    let report_1 = setInterval(()=>{
      this.now.date = moment.unix(String(this.now.unix_ts).split('.')[0])._d
      this.now.gmt = new Date(this.now.date).toUTCString()
    },1000)
    this.ids.report_1 = report_1
    this.tdy.stmp = String(timestamp.now()).split('.')[0]

    setInterval(()=>{
      this.now.unix_ts = timestamp.now()
      let now = new Date();

      // Extract hours, minutes, and seconds
      let hours = now.getHours();
      let minutes = now.getMinutes();
      let seconds = now.getSeconds();

      // Determine if it's AM or PM
      let amOrPm = hours >= 12 ? 'PM' : 'AM';

      // Convert hours to 12-hour format
      hours = hours % 12;
      hours = hours ? hours : 12; // Handle midnight (0 hours)

      // Add leading zeros to minutes and seconds if necessary
      minutes = minutes < 10 ? '0' + minutes : minutes;
      seconds = seconds < 10 ? '0' + seconds : seconds;

      // Construct the formatted time string
      let formattedTime = hours + ':' + minutes + ':' + seconds + ' ' + amOrPm;
      this.now.time = formattedTime
      
    },1000)

    this.getInpDate({
      is_load : true
    })
    
  }
};
</script>

<style></style>
