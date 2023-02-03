<template>
    <div>
      <h3>아이템 주요 정보 추출기 사용법</h3>
      <ul id="menual">
        <li>정보를 추출할 파일을 선택</li>
        <li><button>추출</button>을 클릭하여 추출!</li>
        <li><button>txt파일로 다운 받기</button>를 클릭하여 다운받기</li>
      </ul>
      <div id="main-page">
        <input type="file" @change="handleFileChange">
        <button @click="extract" style="margin-right: 7px;">추출</button>
        <button @click="downloadTxtFile">txt파일로 다운받기</button>
      </div>
    </div>
</template>

<script>
export default {
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
      extract() {
        var fr = new FileReader();
        fr.onload = e => {
          let inputData = e.target.result; 
          let datas = this.bindInputData(inputData);
          console.log(datas);
        
          this.outputData = "";
          datas.forEach(_data => {
            this.outputData += _data + '\n';
          });
  
          alert("추출이 완료되었습니다!");
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
  
        splitted.forEach(row=> {
            const splitted_row = row.split(',');
            let result_str = "";
            if (splitted_row.length >= 5) {
              splitted_row.forEach((col, index) => {
                  if (index === 0 || index === 3 || index === 4) {
                      result_str += col + ',';
                  }

                  if (index === 5) result_str += col;
              });

              result_str = result_str.replaceAll('\n', '');
              result_str = result_str.replaceAll('\r', '');
              datas.push(result_str);
            }      
        });
  
        return datas;
      },
    }
}
</script>

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