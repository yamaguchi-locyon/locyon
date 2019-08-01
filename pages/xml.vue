<template>
  <ul>
    <li v-for="entry of entries" :key="entry.id" class="item">
      <a href="#"><span class="date">{{entry.date}}</span><span class="title">{{entry.title}}</span></a>
    </li>
  </ul>
</template>

<script>
export default {
  data () {
    return {
      entries: []
    }
  },
  created () {
    $.ajax({
      url: 'news.xml',
      dataType: 'xml'
    }).done((xml) => {
      const items = xml.getElementsByTagName('item');
      let entries = [];

      for (let i = 0, nItems = items.length; i < nItems; i += 1) {
        const id = items[i].getElementsByTagName('entryID')[0].textContent;
        const title = items[i].getElementsByTagName('entryTitle')[0].textContent;
        const date = items[i].getElementsByTagName('entryDate')[0].textContent;
        entries.push({
          index: i,
          id: id,
          title: title,
          date: date
        });
      }

      this.entries = entries;
    });
  },
};
</script>

<style>
</style>
