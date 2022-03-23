<template>
  <div class="studies-content bg-blue-grey-1">
    <div class="row justify-between full-width q-mb-lg">
      <div class="top-studies col-4">
        <h1 class="text-h4 blue-grey-12 q-mb-xs">Studies</h1>
        <q-breadcrumbs class="breadcrumbs">
          <template v-slot:separator>
            <q-icon size="1.5em" name="chevron_right" color="grey" />
          </template>
          <q-breadcrumbs-el
            class="text-grey"
            label="Home"
            icon="home"
          ></q-breadcrumbs-el>
          <q-breadcrumbs-el class="text-grey">
            <span class="material-icons"> perm_media </span>
            <p class="align-icon-text">Studies</p>
          </q-breadcrumbs-el>
        </q-breadcrumbs>
      </div>
      <div class="top-studies col-4 q-pt-xl q-pb-md text-right">
        <q-btn unelevated color="light-blue-10">
          <span class="material-icons"> add </span>
          <p class="align-icon-text">Add a study</p>
        </q-btn>
        <q-btn unelevated>
          <span class="material-icons more"> more_vert </span>
        </q-btn>
      </div>
    </div>
    <div>
      <q-table
        :rows="studies"
        :columns="columns"
        row-key="name"
        :visible-columns="visibleColumns"
        hide-bottom
        :rows-per-page-options="[0]"
        v-model:pagination="pagination"
      >
        <template v-slot:top>
          <div class="row justify-between full-width">
            <div class="col-4">
              <q-select
                dense
                v-model="visibleColumns"
                outlined
                :options="options"
                label="Select a sponsor"
                options-cover
              />
            </div>
            <div class="col-4 q-mr-md">
              <q-input
                dense
                outlined
                debounce="300"
                v-model="filter"
                placeholder="Search for study name"
                style="min-width: 10%"
              >
                <template v-slot:prepend>
                  <q-icon name="search" />
                </template>
              </q-input>
            </div>
          </div>
        </template>
        <template v-slot:body-cell-action="props">
          <q-td :props="props" class="text-right">
            <q-btn outline color="light-blue-10" label="QC" />
            <q-btn
              class="q-mr-lg"
              no-caps
              outline
              color="light-blue-10"
              label="Evaluation"
            />
          </q-td>
        </template>
        <q-btn v-on:click.stop="onClickFunction" />
      </q-table>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { ref } from "vue";

export default {
  name: "StudiesPage",
  setup() {
    return {
      model: ref(null),
      options: ["Sponsor 1", "Sponsor 2"],
    };
  },
  data() {
    return {
      columns: [
        {
          name: "id",
          field: "id",
          align: "left",
          label: "#",
          sortable: true,
        },
        {
          name: "name",
          field: "name",
          align: "left",
          label: "Name",
          sortable: true,
        },
        {
          name: "sponsor",
          field: "sponsor",
          align: "left",
          label: "Sponsor",
          sortable: true,
        },
        {
          name: "lastActivity",
          field: "lastActivity",
          align: "left",
          label: "Last activity",
          sortable: true,
        },
        {
          name: "action",
          field: "action",
          align: "left",
          sortable: true,
        },
      ],
      studies: [],
      search: "",
      pagination: {
        page: 1,
        rowsPerPage: 0,
      },
    };
  },
  async created() {
    try {
      const res = await axios
        .get("http://localhost:8000/api/studies")
        .then((response) => (this.studies = response.data["hydra:member"]));

      console.log(this.studies);
    } catch (e) {
      console.error(e);
    }
  },
};
</script>
