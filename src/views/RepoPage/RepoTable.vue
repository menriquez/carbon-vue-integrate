<script>
import LinkList from './LinkList';

export default {
  name: 'RepoTable',
  props: {
    headers: Array,
    rows: Array,
    title: String,

    helperText: String,
    loading: Boolean,
    totalRows: Number
  },

  components: { LinkList },

  computed: {
    columns() {
      return this.headers.map(header => header.header);
    },
    data() {
      return this.rows.map(row => ({
        data: [
          row.name,
          row.createdAt,
          row.updatedAt,
          row.issueCount,
          row.stars,
          row.links
        ],
        description: 'Row description'
      }));
    }
  }
};
</script>

<template>
  <div>
    <cv-data-table-skeleton
      v-if="loading"
      :columns="columns"
      :title="title"
      :helper-text="helperText"
      :rows="10"
    />

    <cv-data-table
      v-else
      :columns="columns"
      :title="title"
      :helper-text="helperText"
      :pagination="{ numberOfItems: this.totalRows }"
      @pagination="$emit('pagination', $event)"
    >
      <template slot="data">
        <cv-data-table-row v-for="(row, rowIndex) in data" :key="`${rowIndex}`">
          <!-- <cv-data-table-cell

          v-for="(cell, cellIndex) in row.data"

          :key="`${cellIndex}`"
          >{{ cell }}</cv-data-table-cell
          >-->
          <cv-data-table-cell
            v-for="(cell, cellIndex) in row.data"
            :key="`${cellIndex}`"
          >
            <template v-if="!cell.url">{{ cell }}</template>
            <link-list
              v-else
              :url="cell.url"
              :homepage-url="cell.homepageUrl"
            />
          </cv-data-table-cell>

          <template slot="expandedContent">{{ row.description }}</template>
        </cv-data-table-row>
      </template>
    </cv-data-table>
  </div>
</template>