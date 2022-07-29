<template>
  <i class="search">
    <input v-model="inputJob" @input="submitAutoComplete" type="text" placeholder="검색어를 입력하세요"/>
  </i>
  <div class="autocomplete disabled">
    <div
        style="cursor: pointer"
        v-for="(res,i) in findJob"
        :key="i"
        v-html="findTextBold(res)"
    ></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      list: [
        '백엔드 엔지니어', '프론트엔드 엔지니어', 'iOS개발자', 'Android개발자', 'QA엔지니어', '머신러닝 엔지니어', '데이터 엔지니어',
        '보안 전문가', 'CTO', '임베디드 개발자', '시스템 설계', 'DevOps', '게임개발자'
      ],
      inputJob: null,
      findJob: null,
    }
  },
  methods: {
    submitAutoComplete() {
      const autocomplete = document.querySelector(".autocomplete");
      if (this.inputJob) {
        autocomplete.classList.remove("disabled");
        this.findJob = this.list.filter((skill) => {
          return skill.match(new RegExp("^" + this.inputJob, "i"));
        });
      } else {
        autocomplete.classList.add("disabled");
      }
    },
    findTextBold(res) {
      const findText = res.match(new RegExp("^" + this.inputJob, "i"));
      return res.toString().replace(findText, `<strong>${findText}</strong>`);
    }
  }
}
</script>