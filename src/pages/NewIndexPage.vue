<template>
  <q-drawer v-model="openDrawer" class="q-pt-sm tw-bg-secondarybg dd-scroll" show-if-above>
    <div class="tw-m-5">
      <div class="tw-flex tw-flex-col tw-gap-2 tw-items-center tw-p-5 tw-bg-tertiarybg tw-rounded-3xl">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"
             class="tw-w-9 tw-h-9 tw-text-primarytext">
          <path stroke-linecap="round" stroke-linejoin="round"
                d="M9 12h3.75M9 15h3.75M9 18h3.75m3 .75H18a2.25 2.25 0 002.25-2.25V6.108c0-1.135-.845-2.098-1.976-2.192a48.424 48.424 0 00-1.123-.08m-5.801 0c-.065.21-.1.433-.1.664 0 .414.336.75.75.75h4.5a.75.75 0 00.75-.75 2.25 2.25 0 00-.1-.664m-5.8 0A2.251 2.251 0 0113.5 2.25H15c1.012 0 1.867.668 2.15 1.586m-5.8 0c-.376.023-.75.05-1.124.08C9.095 4.01 8.25 4.973 8.25 6.108V8.25m0 0H4.875c-.621 0-1.125.504-1.125 1.125v11.25c0 .621.504 1.125 1.125 1.125h9.75c.621 0 1.125-.504 1.125-1.125V9.375c0-.621-.504-1.125-1.125-1.125H8.25zM6.75 12h.008v.008H6.75V12zm0 3h.008v.008H6.75V15zm0 3h.008v.008H6.75V18z"/>
        </svg>

        <span class="tw-text-primarytext tw-text-sm tw-font-semibold">Weekly Service Worksheet</span>

          <button @click="$refs.uploaderref.pickFiles(category = 'WeeklyWorkSheet');" type="button"
                  class="tw-rounded-lg tw-border tw-border-hara tw-bg-transparent tw-px-4 tw-py-2 tw-text-sm tw-font-semibold tw-text-hara hover:tw-bg-secondarybg focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">
            Upload
          </button>
      </div>
      <div class="tw-flex tw-flex-col tw-gap-2 tw-items-center tw-mt-3 tw-p-5 tw-bg-tertiarybg tw-rounded-3xl">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"
             class="tw-w-9 tw-h-9 tw-text-primarytext">
          <path stroke-linecap="round" stroke-linejoin="round"
                d="M12 6v12m-3-2.818l.879.659c1.171.879 3.07.879 4.242 0 1.172-.879 1.172-2.303 0-3.182C13.536 12.219 12.768 12 12 12c-.725 0-1.45-.22-2.003-.659-1.106-.879-1.106-2.303 0-3.182s2.9-.879 4.006 0l.415.33M21 12a9 9 0 11-18 0 9 9 0 0118 0z"/>
        </svg>

        <span class="tw-text-primarytext tw-text-sm tw-font-semibold">Current employee payroll rate</span>

          <button @click="$refs.uploaderref.pickFiles(category = 'PayrollRate');" type="button"
                  class="tw-rounded-lg tw-border tw-border-hara tw-bg-transparent tw-px-4 tw-py-2 tw-text-sm tw-font-semibold tw-text-hara hover:tw-bg-secondarybg focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">
            Upload
          </button>
      </div>
      <q-item-label class="tw-text-white tw-mt-9 tw-mb-7 tw-text-base tw-font-normal">My Files</q-item-label>
      <template v-for="(table, index) in tables" :key="index">
        <div class="tw-mb-0.5 tw-w-full tw-flex tw-items-center hover:tw-bg-tertiarybg tw-rounded-xl tw-py-1 tw-px-3"
             :class="selection===table.name ? 'tw-bg-tertiarybg' : 'tw-bg-transparent'">
          <div @click="table['toggle'] = !table['toggle']" class="tw-mr-3 tw-h-full"
               :class="table['toggle'] ? 'rotate' : ''">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                 stroke="currentColor" class="tw-w-5 tw-h-5"
                 :class="selection===table.name ? 'tw-text-hara' : 'tw-text-white'">
              <path stroke-linecap="round" stroke-linejoin="round" d="M8.25 4.5l7.5 7.5-7.5 7.5"/>
            </svg>
          </div>
          <div class="tw-w-full tw-flex tw-items-center tw-justify-between">
            <div class="tw-w-10/12 tw-flex tw-items-center tw-cursor-pointer" @click="selectTable(table.name)">
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                   stroke="currentColor" class="tw-w-5 tw-h-5 tw-mr-3"
                   :class="selection===table.name ? 'tw-text-hara' : 'tw-text-white'">
                <path stroke-linecap="round" stroke-linejoin="round"
                      d="M3.375 19.5h17.25m-17.25 0a1.125 1.125 0 01-1.125-1.125M3.375 19.5h7.5c.621 0 1.125-.504 1.125-1.125m-9.75 0V5.625m0 12.75v-1.5c0-.621.504-1.125 1.125-1.125m18.375 2.625V5.625m0 12.75c0 .621-.504 1.125-1.125 1.125m1.125-1.125v-1.5c0-.621-.504-1.125-1.125-1.125m0 3.75h-7.5A1.125 1.125 0 0112 18.375m9.75-12.75c0-.621-.504-1.125-1.125-1.125H3.375c-.621 0-1.125.504-1.125 1.125m19.5 0v1.5c0 .621-.504 1.125-1.125 1.125M2.25 5.625v1.5c0 .621.504 1.125 1.125 1.125m0 0h17.25m-17.25 0h7.5c.621 0 1.125.504 1.125 1.125M3.375 8.25c-.621 0-1.125.504-1.125 1.125v1.5c0 .621.504 1.125 1.125 1.125m17.25-3.75h-7.5c-.621 0-1.125.504-1.125 1.125m8.625-1.125c.621 0 1.125.504 1.125 1.125v1.5c0 .621-.504 1.125-1.125 1.125m-17.25 0h7.5m-7.5 0c-.621 0-1.125.504-1.125 1.125v1.5c0 .621.504 1.125 1.125 1.125M12 10.875v-1.5m0 1.5c0 .621-.504 1.125-1.125 1.125M12 10.875c0 .621.504 1.125 1.125 1.125m-2.25 0c.621 0 1.125.504 1.125 1.125M13.125 12h7.5m-7.5 0c-.621 0-1.125.504-1.125 1.125M20.625 12c.621 0 1.125.504 1.125 1.125v1.5c0 .621-.504 1.125-1.125 1.125m-17.25 0h7.5M12 14.625v-1.5m0 1.5c0 .621-.504 1.125-1.125 1.125M12 14.625c0 .621.504 1.125 1.125 1.125m-2.25 0c.621 0 1.125.504 1.125 1.125m0 1.5v-1.5m0 0c0-.621.504-1.125 1.125-1.125m0 0h7.5"/>
              </svg>
              <span style="width:138px;" class="tw-flex-1 tw-text-white tw-text-base tw-overflow-hidden tw-text-ellipsis">{{ table.name }}</span>
            </div>
            <div class="tw-w-2/12" @click="deleteTable(table.name, index)">
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                   stroke="currentColor" class="tw-w-5 tw-h-5 tw-ml-3 tw-text-red-500 hover:tw-text-red-400">
                <path stroke-linecap="round" stroke-linejoin="round"
                      d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0"/>
              </svg>
            </div>
          </div>
        </div>
        <q-slide-transition>
          <div v-show="table['toggle']" class="tw-w-full tw-py-1">
            <div v-for="(col, col_index) in table['children']" :key="col_index">
              <div class="tw-flex tw-items-center tw-pl-12 tw-my-2">
                <q-icon :name="col.icon" size="xs" color="white"/>
                <span class="tw-ml-2 tw-text-white tw-text-sm">
                  {{ col.label }}
                </span>
              </div>
            </div>
          </div>
        </q-slide-transition>
      </template>
      <div v-if="tables.length===0" class="tw-flex tw-items-center">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"
             class="tw-w-6 tw-h-6 tw-text-primarytext tw-mr-2">
          <path stroke-linecap="round" stroke-linejoin="round"
                d="M12 9v3.75m-9.303 3.376c-.866 1.5.217 3.374 1.948 3.374h14.71c1.73 0 2.813-1.874 1.948-3.374L13.949 3.378c-.866-1.5-3.032-1.5-3.898 0L2.697 16.126zM12 15.75h.007v.008H12v-.008z"/>
        </svg>
        <span class="tw-text-primarytext">No files available</span>
      </div>
    </div>
  </q-drawer>
  <q-uploader
    label="Individual upload"
    style="max-width: 300px"
    @added="files"
    class="float-right tw-hidden"
    ref="uploaderref"
  >
    <template v-slot:header="scope">
      <div class="row no-wrap items-center q-pa-sm q-gutter-xs">
        <q-btn v-if="scope.queuedFiles.length > 0" icon="clear_all" @click="scope.removeQueuedFiles" round dense flat>
          <q-tooltip>Clear All</q-tooltip>
        </q-btn>
        <q-btn v-if="scope.uploadedFiles.length > 0" icon="done_all" @click="scope.removeUploadedFiles" round dense
               flat>
          <q-tooltip>Remove Uploaded Files</q-tooltip>
        </q-btn>
        <q-spinner v-if="scope.isUploading" class="q-uploader__spinner"/>
        <div class="col">
          <div class="q-uploader__title">Upload your files</div>
          <div class="q-uploader__subtitle">{{ scope.uploadSizeLabel }} / {{ scope.uploadProgressLabel }}</div>
        </div>
        <q-btn v-if="scope.canAddFiles" type="a" icon="add_box" @click="scope.pickFiles" round dense flat>
          <q-uploader-add-trigger/>
          <q-tooltip>Pick Files</q-tooltip>
        </q-btn>
        <q-btn v-if="scope.canUpload" icon="cloud_upload" @click="upload" round dense flat>
          <q-tooltip>Upload File</q-tooltip>
        </q-btn>

        <q-btn v-if="scope.isUploading" icon="clear" @click="scope.abort" round dense flat>
          <q-tooltip>Abort Upload</q-tooltip>
        </q-btn>
      </div>
    </template>
  </q-uploader>
  <q-page class="q-pa-sm tw-bg-dark tw-flex tw-flex-col">
    <q-card-section class="tw-flex-1">
      <div class="tw-flex tw-justify-end tw-mb-3 tw-gap-3">
        <button @click="downloadSamplePayroll" type="button"
                class="tw-rounded-lg tw-bg-hara hover:tw-bg-morehara tw-px-3.5 tw-py-1.5 tw-text-sm tw-font-semibold tw-text-black">
          Download Sample Payroll sheet
        </button>
        <button @click="download_xlsx" type="button"
                class="tw-rounded-lg tw-bg-hara hover:tw-bg-morehara tw-px-3.5 tw-py-1.5 tw-text-sm tw-font-semibold tw-text-black">
          Download Results
        </button>
        <button @click="openAddWorkingDatesDialog" type="button"
                class="tw-rounded-lg tw-bg-hara hover:tw-bg-morehara tw-px-3.5 tw-py-1.5 tw-text-sm tw-font-semibold tw-text-black">
          Add Working Dates
        </button>
      </div>
      <q-tabs
      v-model="activeTab"
      dense
      class="text-grey"
      active-color="tw-text-morehara"
      indicator-color="tw-text-morehara"
      align="justify"
      narrow-indicator
      no-caps
    >
      <q-tab name="tab1" :label="selection || 'Tab 1'" class="tw-text-hara" />
      <q-tab name="tab2" label="Weekly Activity Report" class="tw-text-hara" />
      <q-tab name="tab3" label="Final Report" class="tw-text-hara" />
    </q-tabs>

    <q-tab-panels v-model="activeTab"           dark
    flat animated>
      <q-tab-panel name="tab1"  class="q-pa-none">
        <q-table
          dark
          flat
          color="#101010"
          :rows="rows"
          row-key="name"
          class="dd-scroll tw-rounded-xl tw-border tw-border-editorborder"
        >
          <!-- Table content for Tab 1 -->
          <template v-slot:header="props">
            <q-tr :props="props" class="tw-bg-primarybg tw-border-b">
              <q-th
                v-for="col in props.cols"
                :key="col.name"
                :props="props"
                class="tw-text-sm tw-font-normal tw-text-primarytext"
              >
                {{ col.label }}
              </q-th>
            </q-tr>
          </template>
          <template v-slot:body="props">
            <q-tr :props="props" :class="props.pageIndex % 2 === 0 ? 'tw-bg-tablebg' : 'tw-bg-primarybg'">
              <q-td
                v-for="col in props.cols"
                :key="col.name"
                :props="props"
                class="tw-text-sm tw-font-normal tw-text-primarytext"
              >
                {{ props.row[col.name] }}
              </q-td>
            </q-tr>
          </template>
        </q-table>
      </q-tab-panel>

      <q-tab-panel name="tab2" class="q-pa-none">
        <q-table
          dark
          flat
          color="#101010"
          :rows="rows3"
          row-key="name"
          class="dd-scroll tw-rounded-xl tw-border tw-border-editorborder"
        >
                    <!-- Table content for Tab 2 -->
           <template v-slot:header="props">
            <q-tr :props="props" class="tw-bg-primarybg tw-border-b">
              <q-th
                v-for="col in props.cols"
                :key="col.name"
                :props="props"
                class="tw-text-sm tw-font-normal tw-text-primarytext"
              >
                {{ col.label }}
              </q-th>
            </q-tr>
          </template>
          <template v-slot:body="props">
            <q-tr :props="props" :class="[
              props.pageIndex % 2 === 0 ? 'tw-bg-tablebg' : 'tw-bg-primarybg',
              getSharedDriverRowClass(props.rowIndex)
            ]">
              <q-td
                v-for="col in props.cols"
                :key="col.name"
                :props="props"
                class="tw-text-sm tw-font-normal tw-text-primarytext"
              >
                {{ props.row[col.name] }}
              </q-td>
            </q-tr>
          </template>
        </q-table>
      </q-tab-panel>

      <q-tab-panel name="tab3" class="q-pa-none">
        <q-table
          dark
          flat
          color="#101010"
          :rows="final_report"
          row-key="name"
          class="dd-scroll tw-rounded-xl tw-border tw-border-editorborder"
        >
          <template v-slot:header="props">
            <q-tr :props="props" class="tw-bg-primarybg tw-border-b">
              <q-th
                v-for="col in props.cols"
                :key="col.name"
                :props="props"
                class="tw-text-sm tw-font-normal tw-text-primarytext"
              >
                {{ col.label }}
              </q-th>
            </q-tr>
          </template>
          <template v-slot:body="props">
            <q-tr :props="props" :class="props.pageIndex % 2 === 0 ? 'tw-bg-tablebg' : 'tw-bg-primarybg'">
              <q-td
                v-for="col in props.cols"
                :key="col.name"
                :props="props"
                class="tw-text-sm tw-font-normal tw-text-primarytext"
              >
                {{ props.row[col.name] }}
              </q-td>
            </q-tr>
          </template>
        </q-table>
      </q-tab-panel>
    </q-tab-panels>
    </q-card-section>
    <div class="tw-flex">
      <div class="tw-flex-grow text-white">

      </div>
      <div class="tw-flex text-white">
        <span>Powered by DuckDB </span>
        <div class="bg-white q-pa-sm tw-flex-auto q-ml-sm">
          <img style="width:50px" class="tw-rounded-lg" src="DuckDB_Logo.png"/>
        </div>
      </div>
    </div>

    <q-dialog v-model="getStartedDialog">
      <q-card class="get-started-card tw-bg-editorborder ">

        <q-card-section class="tw-text-primarytext" style="padding:20px 0px 0 0px">
          <div>
            <q-carousel
              v-model="slide"
              transition-prev="scale"
              transition-next="scale"
              swipeable
              animated
              control-color="white"
              prev-icon="arrow_left"
              next-icon="arrow_right"
              navigation-icon="radio_button_unchecked"
              navigation
              padding
              arrows
              height="500px"
              class="tw-bg-editorborder text-white rounded-borders"
            >
              <template v-slot:navigation-icon="{ active, btnProps, onClick }">
                <q-btn v-if="active" size="sm" icon="radio_button_checked" class="tw-text-hara" flat round dense @click="onClick" />
                <q-btn v-else size="xs" :icon="btnProps.icon" color="white" flat round dense @click="onClick" />
              </template>
              <q-carousel-slide name="step_1"  class="column no-wrap flex-center">
                 <img src="step1.png" class="tw-w-full tw-h-full">
                 <div class="q-mt-md text-center tw-text-hara tw-text-base">
                    {{ step_1 }}
                  </div>

              </q-carousel-slide>
              <q-carousel-slide name="step_2" class="column no-wrap flex-center">
                <img src="step2.png" class="tw-w-full ">
                <div class="q-mt-md text-center tw-text-hara tw-text-base">
                  {{ step_2 }}
                </div>
              </q-carousel-slide>
              <q-carousel-slide name="step_3" class="column no-wrap flex-center">
                <div class="q-mt-md text-center tw-text-hara tw-text-base">
                  {{ step_3 }}
                </div>
              </q-carousel-slide>
              <q-carousel-slide name="step_4" class="column no-wrap flex-center">
                <div class="q-mt-md text-center tw-text-hara tw-text-base">
                  {{ step_4 }}
                </div>
              </q-carousel-slide>
            </q-carousel>
          </div>
        </q-card-section>
        <q-card-actions class="justify-center tw-pb-lg" style="padding-top:20px">
          <button
            @click="getStarted()"
            class="tw-bg-hara  tw-px-20 tw-py-3 tw-font-semibold tw-rounded-lg">
            Get Started
          </button>
        </q-card-actions>
      </q-card>
    </q-dialog>

    <!-- Add Working Dates Dialog -->
    <q-dialog v-model="addWorkingDatesDialog" persistent>
      <q-card style="min-width: 350px" class="tw-bg-editorborder">
        <q-card-section>
          <div class="text-h6 tw-text-primarytext">Add Working Dates</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          <q-select
            v-model="selectedDriver"
            :options="driverOptions"
            label="Select Driver"
            class="q-mb-md"
            dark
            outlined
          />
          <q-select
            v-model="selectedDates"
            :options="availableDates"
            label="Select Dates"
            multiple
            use-chips
            dark
            outlined
          />
        </q-card-section>

        <q-card-actions align="right" class="text-primary">
          <q-btn flat label="Cancel" v-close-popup />
          <q-btn flat label="Add" @click="addWorkingDates" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>
  </q-page>
</template>

<script>
import { defineComponent, ref } from 'vue'
import * as XLSX from 'xlsx/xlsx.mjs';
import { saveAs } from 'file-saver';
import { VAceEditor } from 'vue3-ace-editor';
import './ace-config';
import sample_csv from '../assets/customers-100.csv?raw';
import sample_payroll from '../assets/payroll.csv?raw';
import "vue-easytable/libs/theme-default/index.css";
import VueEasytable from "vue-easytable";

export default defineComponent({
  name: 'NewIndexPage',
  data() {
    return {
      file: ref([]),
      worksheet_file: ref([]),
      columns: [],
      rows: [],
      query: ref(''),
      tables: ref([]), /*contains objects with keys {name, length, columns} */
      selection: ref(''),
      getStartedDialog: ref(false),
      slide: ref('step_1'),
      step_1: ref('Upload current payroll wage policy'),
      step_2: ref("Upload current weekly service worksheet(download from MGBA)"),
      step_3: ref("Check on activity entry and final report"),
      step_4: ref("Download the summarized report in one click"),
      openDrawer: ref(false),
      tableNameSuggestions: ["table1", "table2", "table3"],
      counter:0,
      sample_csv: ref(sample_csv),
      sample_payroll: ref(sample_payroll),
      activeTab: 'tab1',
      rows1: [],
      rows2: [],
      filled_rows: [],
      final_report: [],
      rows3: [],
      shared_route_row_index: [],
      shared_route_driver_index: [],
      highlightedRows: [1, 3, 5], // List of row numbers to highlight (0-based index)
      addWorkingDatesDialog: ref(false),
      selectedDriver: ref(null),
      selectedDates: ref([]),
      driverOptions: [],
      availableDates: [],
    }
  },
  components: {
    VAceEditor,
    VueEasytable,
  },
  async created() {
    this.openPopUp();
    this.$bus.on('openPopUp', this.openPopUp)
    this.openDrawer = this.$q.platform.is.desktop ? true : false;
  },
  methods: {
    initializeEditor(editor) {
      let self = this;
      // Define a custom autocomplete function
      editor.completers.push({
        getCompletions: function (editor, session, pos, prefix, callback) {
          callback(null, self.tables.map(function (table) {
            return {
              caption: table.name,
              value: table.name,
              meta: "table"
            };
          }));
        }
      });
      self.tables.filter(function (item) {
        editor.completers.push({
          getCompletions: function (editor, session, pos, prefix, callback) {
            callback(null, item.children.map(function (col) {
              return {
                caption: col.label,
                value: col.label,
                meta: "column"
              };
            }));
          }
        });
        return item
      })
    },
    selectTable(name) {
      this.selection = name
      this.query = `SELECT * FROM ${name};`
      this.search();
    },
    files(files) {
      this.file = files[0];
      this.upload(this.category);
    },
    pickFiles(category) {
      // Store the file type for later use
      this.category = category;
      // Call the original pickFiles method
      this.$refs.uploaderref.$el.pickFiles();
    },


    async upload() {
      console.log(this.category)
      this.columns = []
      let fileReader = new FileReader();
      let text = "";
      let name = this.file.name.split(".")[0];
      let fileType = this.file.name.split(".")[1].toLowerCase();

      name = name.replace(/[^a-zA-Z0-9]/g, "_");

      if (fileType === 'xls' || fileType === 'xlsx') {
        fileReader.onload = async (e) => {
          const data = new Uint8Array(e.target.result);
          const workbook = XLSX.read(data, {type: 'array'});
          const firstSheetName = workbook.SheetNames[0];
          const worksheet = workbook.Sheets[firstSheetName];
          text = XLSX.utils.sheet_to_csv(worksheet);
          await this.processCSV(this.category, text);
        };
        fileReader.readAsArrayBuffer(this.file);
      } else if (fileType === 'csv') {
        fileReader.onload = async () => {
          text = fileReader.result;
          await this.processCSV(this.category, text);
        };
        fileReader.readAsText(this.file);
      } else {
        this.$refs.uploaderref.reset();
        this.$q.notify({type: 'negative', message: `Apologies! At this moment we only support CSV, XLS, and XLSX files.`, position: 'top'});
        return;
      }
    },

    async processCSV(name, text) {
      let self = this;
      let tableExists = false;

      await self.$db.registerFileText("sample_table.csv", text);
      self.tables.forEach((table) => {
        if (table.name == name) {
          tableExists = true;
        }
      });

      if (tableExists) {
        // Instead of using a dialog, we'll use a confirm method
        if (!confirm(`Table "${name}" already exists. Do you want to replace it?`)) {
          self.$refs.uploaderref.reset();
          self.$q.notify({type: 'info', message: `Upload cancelled`, position: 'top'});
          return;
        }
        // If we reach here, user clicked OK
        // Remove the existing table from the list
      }

      self.$q.loading.show();
      try {
        // Drop the existing table if it exists
        await self.$conn.query(`DROP TABLE IF EXISTS raw_${name};`);
        let query;
        if (name === 'WeeklyWorkSheet') {
          query = `CREATE TABLE raw_${name} AS
          SELECT *
          FROM read_csv_auto('sample_table.csv', header=true, skip=3);`;
        } else if (name === 'PayrollRate') {
          query = `CREATE TABLE raw_${name} AS
          SELECT *
          FROM read_csv_auto('sample_table.csv');`;
        } else {
          query = `CREATE TABLE raw_${name} AS
          SELECT *
          FROM read_csv_auto('sample_table.csv');`;
        }

        await self.$conn.query(query);
        self.$refs.uploaderref.reset();

        const stmt1 = await self.$conn.prepare(`SELECT CAST(COUNT(*) AS INT)
                                                FROM raw_${name}`)
        const res1 = await stmt1.query()
        const stmt2 = await self.$conn.prepare(`SELECT COLUMN_NAME, DATA_TYPE
                                                FROM INFORMATION_SCHEMA.COLUMNS
                                                WHERE TABLE_NAME = 'raw_${name}'`)
        const res2 = await stmt2.query()
        let len = Object.values(JSON.parse(JSON.stringify(res1.toArray()))[0])[0]
        let columns = JSON.parse(JSON.stringify(res2.toArray()))
        console.log(columns)
        // Verify columns
        const expectedColumns = {
          'WeeklyWorkSheet': ['Date', 'WA Name', 'Svc Area #', 'Veh #', 'Driver/ Helper Name'],
          'PayrollRate': ['NAME', 'FEDEX ID', 'Rate by Day', 'Rate by Week'],
          // Add more expected column sets for other table types if needed
        };

        const tableColumns = columns.map(col => col.column_name.toLowerCase());

        if (expectedColumns[name]) {
          const missingColumns = expectedColumns[name].filter(col => !tableColumns.includes(col.toLowerCase()));

          if (missingColumns.length > 0) {
            let errorMessage = `Table "${name}" is missing required columns: ${missingColumns.join(', ')}.`;
            throw new Error(errorMessage);
            return;
          }
        }

        self.tables = self.tables.filter(t => t.name !== name);
        await self.$conn.query(`DROP TABLE IF EXISTS ${name};`);
        await self.$conn.query(`
            CREATE TABLE ${name} AS
            SELECT * FROM raw_${name};
          `);

        // Drop the raw table after updating the target table
        await self.$conn.query(`DROP TABLE IF EXISTS raw_${name};`);

        self.selectTable(name);
        // Copy data to appropriate rows based on table name
        if (name === 'WeeklyWorkSheet') {
          const dataQuery = await self.$conn.prepare(`SELECT * FROM ${name}`);
          const dataResult = await dataQuery.query();
          self.rows1 = JSON.parse(JSON.stringify(dataResult.toArray()));
          self.fileWorksheet();
        } else {
          const dataQuery = await self.$conn.prepare(`SELECT * FROM ${name}`);
          const dataResult = await dataQuery.query();
          self.rows2 = JSON.parse(JSON.stringify(dataResult.toArray()));
          if (self.rows2.length > 0 && self.rows1.length > 0) {
            self.fileWorksheet();
          }
        }
        self.tables.push({
          name: name, header: 'root', toggle: false, length: len, children: columns.map((obj) => {
            let icon = 'tag'
            if (["BIGINT","INTEGER"].includes(obj['data_type'])) {
              icon = 'tag'
            }
            else if (obj['data_type'] === "VARCHAR") {
              icon = 'abc'
            } else if (['DATE',"TIMESTAMP"].includes(obj['data_type'])) {
              icon = 'calendar_month'
            }
            return {label: obj['column_name'], icon: icon, header: 'generic'}
          })
        })
        self.$q.notify({type: 'positive', message: `Table "${name}" ${tableExists ? 'replaced' : 'created'} successfully`, position: 'top'});
      } catch (error) {
        console.error('Error processing CSV:', error);
        self.$q.notify({type: 'negative', message: `Error processing CSV: ${error.message}`, position: 'top'});
      } finally {
        self.$q.loading.hide();
        self.counter++;
      }
    },

    async fileSharedRoute(){
      for (let i = 0; i < this.rows1.length; i++) {
        const currentRow = this.rows1[i];
        this.rows1[i]['rowID'] = i;
        this.rows1[i]['Shared Route'] = false;
        // Check if this is a potential shared driver row
        if (!currentRow['Date'] && !currentRow['WA Name'] && currentRow['Driver/ Helper Name']) {
          let totalRow = this.rows1[i - 1];
          let j = i;
          let sumActDelStps = 0;
          let sumActDelPkgs = 0;
          let sumActPUStps = 0;
          let sumActPUPkgs = 0;

          // Look for the end of shared drivers and sum up their values
          while (j < this.rows1.length && (!this.rows1[j]['Date'] && !this.rows1[j]['WA Name'] && currentRow['Driver/ Helper Name'])) {
            this.rows1[j]['rowID'] = j;
            sumActDelStps += parseInt(this.rows1[j]['Act Del Pkgs'] || 0);
            sumActDelPkgs += parseInt(this.rows1[j]['Act PU Stps'] || 0);
            sumActPUStps += parseInt(this.rows1[j]['Act PU Pkgs'] || 0);
            sumActPUPkgs += parseInt(this.rows1[j]['ILS%'] || 0);
            j++;
          }

          // Verify if the sum matches the total row
          if (sumActDelStps === parseInt(totalRow['Act Del Stps'] || 0) &&
              sumActDelPkgs === parseInt(totalRow['Act Del Pkgs'] || 0) &&
              sumActPUStps === parseInt(totalRow['Act PU Stps'] || 0) &&
              sumActPUPkgs === parseInt(totalRow['Act PU Pkgs'] || 0)) {

            this.rows1[i - 1]['Shared Route'] = true;
            this.rows1[i - 1]['Driver/ Helper Name'] = "%SHARED ROUTE%";
            // Correct shared driver rows and add their indices
            for (let k = i; k < j && k < this.rows1.length; k++) {
              this.rows1[k]['Date'] = totalRow['Date'];
              this.rows1[k]['WA Name'] = totalRow['WA Name'];
              this.rows1[k]['Act Del Stps'] = parseInt(this.rows1[k]['Act Del Pkgs'] || 0);
              this.rows1[k]['Act Del Pkgs'] = parseInt(this.rows1[k]['Act PU Stps'] || 0);
              this.rows1[k]['Act PU Stps'] = parseInt(this.rows1[k]['Act PU Pkgs'] || 0);
              this.rows1[k]['Act PU Pkgs'] = parseInt(this.rows1[k]['ILS%'] || 0);
              this.rows1[k]['ILS%'] = 0;
              this.rows1[k]['Shared Route'] = true;
            }
            i = j - 1;  // Move to the last processed row
          }
        }
      }
      // store to duckdb table named filled_worksheet
    // Store rows1 data into a new table named filled_worksheet, filtering out rows with empty 'Driver/ Helper Name'


      this.$db.registerFileText("filled_worksheet.json", JSON.stringify(this.rows1));
      await this.$conn.query(`DROP TABLE IF EXISTS filled_worksheet;`)
      await this.$conn.insertJSONFromPath("filled_worksheet.json", { name: "filled_worksheet", create: true})

      // Fetch the updated data back into rows1 Date	WA Name	Svc Area #	Driver/ Helper Name	WA#	Act Del Stps	Act Del Pkgs	Act PU Stps	Act PU Pkgs
      const result = await this.$conn.query(`SELECT Date, "WA Name", "Svc Area #", "Driver/ Helper Name", "WA#", "Act Del Stps", "Act Del Pkgs", "Act PU Stps", "Act PU Pkgs", "Shared Route" FROM filled_worksheet where "Driver/ Helper Name" != '' ORDER BY rowID ASC;`);
      this.rows3 = JSON.parse(JSON.stringify(result.toArray()));

      // Query the filled_worksheet Fetch shared route rows and driver rows index
      // Query to fetch shared route rows and driver rows index
      for (let i = 0; i < this.rows3.length; i++) {
        if (this.rows3[i]['Shared Route']) {
          if (this.rows3[i]['Driver/ Helper Name'] === '%SHARED ROUTE%') {
            this.shared_route_row_index.push(i);
          } else {
            this.shared_route_driver_index.push(i);
          }
        }

      }
    },

    async notifyUnmatchedNames(){
      const filledWorksheetNames = await this.$conn.query(`
          SELECT DISTINCT "Driver/ Helper Name"
          FROM filled_worksheet
          WHERE "Driver/ Helper Name" != '%SHARED ROUTE%'
        `);

        // Get names from PayrollRate table
        const payrollRateNames = await this.$conn.query(`
          SELECT "Fedex Name" AS name FROM PayrollRate
          UNION
          SELECT "Name" AS name FROM PayrollRate
        `);

        // Find names in filled_worksheet that don't exist in PayrollRate
        const unmatchedNames = filledWorksheetNames.toArray().filter(worksheetName => {
          if (worksheetName['Driver/ Helper Name'] === '%SHARED ROUTE%') {
            return false; // Exclude SHARED ROUTE from unmatched names
          }
          return !payrollRateNames.toArray().some(payrollName =>
            payrollName.name.toLowerCase() === worksheetName['Driver/ Helper Name'].toLowerCase()
          );
        });

        if (unmatchedNames.length > 0) {
          console.log('Unmatched names:', unmatchedNames);

          // Notify user about unmatched names
          const unmatchedNamesString = unmatchedNames.map(name => name['Driver/ Helper Name']).join(', ');
          this.$q.notify({
            message: `The following names from the worksheet are not found in the PayrollRate table: ${unmatchedNamesString}`,
            color: 'warning',
            position: 'top',
            timeout: 5
          });
        }
      },

    async fileFedexIDAndSalary() {
      if (this.rows2.length > 0) {
        // Get unique names from filled_worksheet
        await this.notifyUnmatchedNames();
        // Join filled_worksheet with PayrollRate based on matched names, including aliases
        await this.$conn.query(`DROP TABLE IF EXISTS final_report;`)
        const joinedQuery = `
          CREATE TABLE final_report AS
          SELECT
            fw."Date" as "Date",
            fw."WA Name" as "WA Name",
            fw."Svc Area #" as "Svc Area #",
            fw."Driver/ Helper Name" as "Driver/ Helper Name",
            fw."WA#" as "WA#",
            fw."Act Del Stps" as "Act Del Stps",
            fw."Act Del Pkgs" as "Act Del Pkgs",
            fw."Act PU Stps" as "Act PU Stps",
            fw."Act PU Pkgs" as "Act PU Pkgs",
            fw."Shared Route" as "Shared Route",
            CASE
              WHEN LOWER(fw."Driver/ Helper Name") = '%shared route%' THEN NULL
              ELSE pr."FEDEX ID"
            END AS "Fedex ID",
            CASE
              WHEN LOWER(fw."Driver/ Helper Name") = '%shared route%' THEN NULL
              ELSE pr."Rate By Day"
            END AS "Rate By Day",
            CASE
              WHEN LOWER(fw."Driver/ Helper Name") = '%shared route%' THEN NULL
              ELSE pr."Rate By Week"
            END AS "Rate By Week",
            false AS "Manipulated"
          FROM
            filled_worksheet fw
          LEFT JOIN
            PayrollRate pr ON
              LOWER(fw."Driver/ Helper Name") = LOWER(pr."FEDEX NAME") OR
              LOWER(fw."Driver/ Helper Name") = LOWER(pr."NAME") OR
              LOWER(fw."Driver/ Helper Name") = '%SHARED ROUTE%'
          WHERE "Driver/ Helper Name" != ''
          ORDER BY
            fw.rowID;
        `;
        console.log(joinedQuery);
        await this.$conn.query(joinedQuery);

        // Fetch data from the materialized table
        const result = await this.$conn.query('SELECT * FROM final_report');

        // Update rows3 with the result from the materialized table
        this.rows3 = JSON.parse(JSON.stringify(result.toArray()));
        console.log(this.rows3);
      }
    },
    async generateReport() {
      try {
        await this.$conn.query('DROP TABLE IF EXISTS date_count;');
        // Step 1: Create a table with count of distinct dates, Manipulated status, and rates
        const createCountTable = `
          CREATE TABLE date_count AS
          SELECT
            "Driver/ Helper Name",
            COUNT(DISTINCT "Date") AS "COUNTA of Date",
            MAX(CASE WHEN "Manipulated" = true THEN 1 ELSE 0 END) AS "Manipulated",
            MAX(CASE
              WHEN "Rate By Day" LIKE '$%' THEN CAST(REPLACE(REPLACE("Rate By Day", '$', ''), ',', '') AS REAL)
              WHEN "Rate By Day" LIKE '%.%' THEN CAST("Rate By Day" AS REAL)
              ELSE CAST("Rate By Day" AS REAL)
            END) AS "Rate By Day",
            MAX(CASE
              WHEN "Rate By Week" LIKE '$%' THEN CAST(REPLACE(REPLACE("Rate By Week", '$', ''), ',', '') AS REAL)
              WHEN "Rate By Week" LIKE '%.%' THEN CAST("Rate By Week" AS REAL)
              ELSE CAST("Rate By Week" AS REAL)
            END) AS "Rate By Week"
          FROM final_report
          WHERE "Driver/ Helper Name" != '%SHARED ROUTE%'
          GROUP BY "Driver/ Helper Name";
        `;
        await this.$conn.query(createCountTable);

        // Step 2: SQL query to calculate weekly salaries and other fields
        const weeklyReportQuery = `
          SELECT
            "Driver/ Helper Name",
            "COUNTA of Date",
            '$' || PRINTF('%.2f',
              CASE
                WHEN "Rate By Week" > 0
                THEN "Rate By Week"
                ELSE "COUNTA of Date" * "Rate By Day"
              END
            ) AS "SUM of WAGES",
            LEAST("COUNTA of Date" * 8, 40) AS "REG HRS",
            PRINTF('%.2f',
              GREATEST(
                (CASE
                  WHEN "Rate By Week" > 0
                  THEN "Rate By Week"
                  ELSE "COUNTA of Date" * "Rate By Day"
                END - (LEAST("COUNTA of Date" * 8, 40) * 15)) / (15 * 1.5),
                0
              )
            ) AS "OT",
            PRINTF('%.2f',
              LEAST("COUNTA of Date" * 8, 40) +
              GREATEST(
                (CASE
                  WHEN "Rate By Week" > 0
                  THEN "Rate By Week"
                  ELSE "COUNTA of Date" * "Rate By Day"
                END - (LEAST("COUNTA of Date" * 8, 40) * 15)) / (15 * 1.5),
                0
              )
            ) AS "TOTAL HRS",
            "Manipulated"
          FROM date_count
          ORDER BY "Driver/ Helper Name";
        `;

        // Execute the query and store the result
        const result = await this.$conn.query(weeklyReportQuery);
        this.final_report = JSON.parse(JSON.stringify(result.toArray(), (key, value) =>
          typeof value === 'bigint' ? value.toString() : value
        ));

        console.log('Weekly report generated:', this.final_report);

        // Clean up: Drop the temporary table
        await this.$conn.query('DROP TABLE IF EXISTS date_count;');
      } catch (error) {
        console.error('Error generating report:', error);
      }
    },

    async fileWorksheet() {
      await this.fileSharedRoute();
      await this.fileFedexIDAndSalary();
      await this.generateReport();
    },

    async search() {
      this.$q.loading.show();
      try {
        const q = await this.$conn.prepare(this.query);
        const r = await q.query();
        const replacer = (key, value) => {
          if (typeof value === 'bigint') {
            return value.toString(); // Convert BigInt to string representation
          }
          return value;
        };
        this.rows = JSON.parse(JSON.stringify(r.toArray(), replacer))
        this.$q.loading.hide();
      } catch (err) {
        this.$q.loading.hide();
        this.$q.notify({
          message: err.message,
          color: 'negative',
          textColor: 'white',
          icon: 'warning',
          position: 'top',
        });

      }
    },
    async deleteTable(name, index) {
      const q = await this.$conn.prepare(`DROP TABLE ${name};`);
      const r = await q.query();
      this.tables.splice(index, 1);
      if (this.tables.length === 0) {
        this.selection = '';
        this.query = '';
        this.rows = [];
        this.final_report = [];
        this.rows3 = [];
        this.shared_route_row_index = [];
        this.shared_route_driver_index = [];
      } else {
        this.selectTable(this.tables[0].name);
      }
      this.$q.notify({type: 'positive', message: `Table with name "${name}" Deleted!!`, position: 'top'})
    },
    handleDrop(e) {
      e.preventDefault();
      this.$refs.uploaderref.addFiles(e.dataTransfer.files);
    },


    download_csv() {
      let self = this;

      function s2ab(s) {
        let buf = new ArrayBuffer(s.length);
        let view = new Uint8Array(buf);
        for (let i = 0; i !== s.length; ++i) view[i] = s.charCodeAt(i) & 0xff;
        return buf;
      }

      let data = self.rows
      const sheet = XLSX.utils.json_to_sheet(data);
      let wbout = XLSX.write({
        SheetNames: ["Sheet1"],
        Sheets: {"Sheet1": sheet}
      }, {
        bookType: 'csv',
        bookSST: true,
        type: 'binary'
      });
      saveAs(new Blob([s2ab(wbout)], {
        type: "application/octet-stream"
      }), `${self.selection}.csv`);
    },

    async download_xlsx() {
      let self = this;

      // Create workbook and worksheets
      let wb = XLSX.utils.book_new();
      let ws1 = XLSX.utils.json_to_sheet(self.final_report);
      let ws2 = XLSX.utils.json_to_sheet(self.rows3);

      // Add worksheets to workbook
      XLSX.utils.book_append_sheet(wb, ws1, "Final Report");
      XLSX.utils.book_append_sheet(wb, ws2, "Weekly Activity Report");

      // Generate XLSX file
      let wbout = XLSX.write(wb, { bookType: 'xlsx', type: 'binary' });

      // Convert binary string to ArrayBuffer
      let buf = new ArrayBuffer(wbout.length);
      let view = new Uint8Array(buf);
      for (let i = 0; i !== wbout.length; ++i) view[i] = wbout.charCodeAt(i) & 0xFF;

      // Use ExcelJS for styling
      const ExcelJS = await import('exceljs');
      let workbook = new ExcelJS.Workbook();
      await workbook.xlsx.load(buf);

      let worksheet = workbook.getWorksheet('Weekly Activity Report');

      // Apply conditional formatting
      const sharedRouteStyle = { fill: { type: 'pattern', pattern: 'solid', fgColor: { argb: 'FFFFFF00' } } }; // Yellow
      const sharedDriverStyle = { fill: { type: 'pattern', pattern: 'solid', fgColor: { argb: 'FF00FF00' } } }; // Green
      const manipulatedStyle = { fill: { type: 'pattern', pattern: 'solid', fgColor: { argb: 'FFFFA500' } } }; // Orange
      self.shared_route_row_index.forEach(index => {
        worksheet.getRow(index + 2).eachCell(cell => {
          cell.style = sharedRouteStyle;
        });
      });

      self.shared_route_driver_index.forEach(index => {
        worksheet.getRow(index + 2).eachCell(cell => {
          cell.style = sharedDriverStyle;
        });
      });

     for (let i = 0; i < self.rows3.length; i++) {
        if (self.rows3[i]['Manipulated'] === true || self.rows3[i]['Manipulated'] === 1) {
          worksheet.getRow(i + 2).eachCell(cell => {
            cell.style = manipulatedStyle;
          });
        }
      }




      // Write to file
      const buffer = await workbook.xlsx.writeBuffer();
      saveAs(new Blob([buffer], { type: 'application/vnd.openxmlformats-officedocument.spreadsheetml.sheet' }), 'report.xlsx');
    },
    openPopUp() {
      this.getStartedDialog = true;
    },
    getStarted(){
      this.getStartedDialog = false,
      this.slide='step_1';
    },
    uploadSampleFile(){
      const blob = new Blob([this.sample_csv], { type: 'text/csv' });
      const file = new File([blob], 'sample.csv', { type: 'text/csv' });
      this.$refs.uploaderref.addFiles([file]);
    },
    downloadSamplePayroll(){
      const blob = new Blob([this.sample_payroll], { type: 'text/csv' });
      const file = new File([blob], 'sample_payroll.csv', { type: 'text/csv' });
      saveAs(file, 'sample_payroll.csv');
    },

    getSharedDriverRowClass(rowIndex) {
      if (this.shared_route_row_index.includes(rowIndex)) {
        return 'shared-route-row';
      } else if (this.shared_route_driver_index.includes(rowIndex)) {
        return 'shared-driver-row';
      }
      return '';
    },
    async openAddWorkingDatesDialog() {
      this.addWorkingDatesDialog = true;
      this.selectedDriver = null;
      this.selectedDates = [];

      // Populate driver options
      this.driverOptions = [...new Set(this.rows3
        .filter(row => row['Driver/ Helper Name'] !== '%SHARED ROUTE%')
        .map(row => row['Driver/ Helper Name']))]
        .map(driverName => ({
          label: driverName,
          value: driverName
        }));

      // Fetch all unique dates from the final_report table
      const result = await this.$conn.query(`
        SELECT DISTINCT Date
        FROM final_report
        ORDER BY Date
      `);

      this.availableDates = result.toArray().map(row => ({
        label: row.Date,
        value: row.Date
      }));
    },
    async addWorkingDates() {
      if (!this.selectedDriver || this.selectedDates.length === 0) return;

      const driver = this.selectedDriver.value;
      const dates = this.selectedDates.map(date => date.value); // Extract just the date values

      try {
        // Find an existing row for the driver to copy data from
        const existingRow = this.rows3.find(row => row['Driver/ Helper Name'] === driver);
        if (!existingRow) {
          throw new Error('No existing data found for the selected driver');
        }

        // Prepare the INSERT statement
        const stmt = await this.$conn.prepare(`
          INSERT INTO final_report (
            "Date", "WA Name", "Svc Area #", "Driver/ Helper Name", "WA#",
            "Act Del Stps", "Act Del Pkgs", "Act PU Stps", "Act PU Pkgs",
            "Shared Route", "Fedex ID", "Rate By Day", "Rate By Week", "Manipulated"
          ) VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?)
        `);

        // Execute the INSERT for each selected date
        const newRows = [];
        for (const date of dates) {
          await stmt.query(
            date,
            existingRow['WA Name'] || '',
            existingRow['Svc Area #'] || '',
            driver,
            existingRow['WA#'] || '',
            0, // Act Del Stps
            0, // Act Del Pkgs
            0, // Act PU Stps
            0, // Act PU Pkgs
            false, // Shared Route
            existingRow['Fedex ID'] || '',
            existingRow['Rate By Day'] || null,
            existingRow['Rate By Week'] || null,
            true // Manipulated
          );

          // Add the new row to our local data
          newRows.push({
            Date: date,
            "WA Name": existingRow['WA Name'] || '',
            "Svc Area #": existingRow['Svc Area #'] || '',
            "Driver/ Helper Name": driver,
            "WA#": existingRow['WA#'] || '',
            "Act Del Stps": 0,
            "Act Del Pkgs": 0,
            "Act PU Stps": 0,
            "Act PU Pkgs": 0,
            "Shared Route": false,
            "Fedex ID": existingRow['Fedex ID'] || '',
            "Rate By Day": existingRow['Rate By Day'] || null,
            "Rate By Week": existingRow['Rate By Week'] || null,
            "Manipulated": true
          });
        }

        // Update local data
        this.rows3 = [...this.rows3, ...newRows];

        // Update final_report data
        await this.generateReport();

        this.$q.notify({
          type: 'positive',
          message: 'Working dates added successfully',
          position: 'top'
        });
      } catch (error) {
        console.error('Error adding working dates:', error);
        this.$q.notify({
          type: 'negative',
          message: 'Error adding working dates: ' + error.message,
          position: 'top'
        });
      }
    },

  },
  // async beforeUnmount() {
  //   await this.$conn.close();
  //   await this.$db.terminate();
  //   await this.$worker.terminate();
  // }
})
</script>
<style scoped>
.rotate{
  transform: rotate(90deg);
  transition-duration: 0.1s;
}

.get-started-card {
  width: 50rem;
  height: 39rem;
  border-radius: 50px;
}

.highlighted-row {
  background-color: #0000ff; /* Changed to blue */
}
.shared-route-row {
  background-color: #b57614; /* Darker yellow for better visibility in dark mode */
  color: #fbf1c7; /* Light beige for better contrast */
}
.shared-driver-row {
  background-color: #458588; /* Brighter blue for better visibility in dark mode */
  color: #fbf1c7; /* Light beige for better contrast */
}
.shared-route-row td,
.shared-driver-row td {
  font-weight: bold; /* Make text bolder for better visibility */
}
</style>
