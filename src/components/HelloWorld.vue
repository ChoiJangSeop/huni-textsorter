<template>
  <div>
    <h3>아이템 순서 정렬기 사용법</h3>
    <ul id="menual">
      <li>파일선택을 통해 정렬할 파일을 선택</li>
      <li><button>정렬</button>을 클릭하여 정렬!</li>
      <li><button>txt파일로 다운 받기</button>를 클릭하여 다운받기</li>
    </ul>
    <div id="main-page">
      <input type="file" @change="handleFileChange">
      <button @click="sort" style="margin-right: 7px;">정렬</button>
      <button @click="downloadTxtFile">txt파일로 다운받기</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',

  data() {
    return {
      file_name: "",
      file: null,
      inputData: "",
      outputData: "",
    }
  },

  methods: {

    handleFileChange(e) {
      let file = e.target.files[0];
      this.file_name = file.name;
      this.file = file;
    },
    sort() {
      var fr = new FileReader();
      fr.onload = e => {
        let inputData = e.target.result; 
        let datas = this.bindInputData(inputData);
        
        datas.sort((a,b) => { return a.priority - b.priority; });

        let splitted = inputData.split('\n');
        this.outputData = "";

        this.outputData += splitted[0] + '\n';
        this.outputData += splitted[1] + '\n';

        datas.forEach(_data => {
          this.outputData += _data.data + '\n';
        });

        this.outputData = this.strEncodeUTF16(this.outputData);

        alert("정렬이 완료되었습니다!");
      }; 
      
      fr.readAsText(this.file);

    },

    downloadTxtFile() {
      var blob = new Blob([this.outputData], { type: 'text/plain' });

      var objURL = window.URL.createObjectURL(blob);
      
      if (window.__Xr_objURL_forCreatingFile__) {
        window.URL.revokeObjectURL(window.__Xr_objURL_forCreatingFile__);
      }
      window.__Xr_objURL_forCreatingFile__ = objURL;

      var a = document.createElement('a');
      a.download = `${this.file_name.split('.')[0]}-sorted.txt`;
      a.href = objURL;
      a.click();

    },

    bindInputData(inputData) {
      let datas = [];

      const splitted = inputData.split('\n');

      splitted.forEach((row, index) => {
        // skip first 2 lines
        if (index !== 0 && index !== 1) {
          const splitted_row = row.split(',');
          let currData = {
            priority: parseInt(splitted_row[0]),
            data: row,
          };

          datas.push(currData);
        }
      });

      return datas;
    },

    strEncodeUTF16(str) {
      var buf = new ArrayBuffer(str.length * 2);
      var bufView = new Uint16Array(buf);

      for (var i=0, strLen=str.length; i < strLen; ++i) {
        bufView[i] = str.charCodeAt(i);
      }
      return bufView;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

#menual {
  background-color: black;
  border: 1px solid white;
  color: white;
  height: 70px;
  width: 400px;
  font-weight: bold;
  margin-left: auto;
  margin-right: auto;
}

#main-page {
  margin-top: 30px;
}

</style>
