<template>
    <div>
      <h3>아이템 지급 파일 변환기 사용법</h3>
      <ul id="menual">
        <li>파일선택을 통해 정렬할 파일을 선택</li>
        <li><button>변환</button>을 클릭하여 정렬!</li>
        <li><button>txt파일로 다운 받기</button>를 클릭하여 다운받기</li>
      </ul>
      <div id="main-page">
        <input type="file" @change="handleFileChange">
        <button @click="convert" style="margin-right: 7px;">변환</button>
        <button @click="downloadTxtFile">txt파일로 다운받기</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'HelloWorld',
  
    data() {
      return {
        colMetaData:"fdItemNum	fdBillingItemID	fdType	fdCharacter	fdPosition	fdItemKind	fdGameMoney	fdFarmPoint	fdCash	fdGuildPoint	fdContributionPoint	fdItemName	fdItemCategory	fdGotRateKind	fdOnOfftype	fdCanUse	fdNotDeleteWhenExpired	fdCanStack	fdNewMark	fdCoupleItemType	fdShowShop	fdPurchasable	fdShowDetailImage	fdDesc	fdRefundable	fdEtc	fdLevel	fdEnable",
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
      convert() {
        var fr = new FileReader();
        fr.onload = e => {
          let inputData = e.target.result; 
          let datas = this.bindInputData(inputData);
          console.log(datas);
        
          this.outputData = "";
          this.outputData += this.colMetaData + '\n';
          datas.forEach(_data => {
            this.outputData += _data + '\n';
          });
  
          alert("변환이 완료되었습니다!");
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
  
        splitted.forEach(row => {
            const splitted_row = row.split(',');
            let result_str = "";
            let len = splitted_row.length;

            splitted_row.forEach((col, index) => {
                
                if (col === "true") col = "1";
                if (col === "false") col = "0";

                if (index >= 0 && index <= 10) {
                    result_str += col + ',';
                } else if (index === 11) {
                    result_str += col.substr(1, col.length-2) + ',';
                } else if (index >= 12 && index <= 22) {
                    result_str += col + ',';
                } else if (index === 23) {
                    result_str += "NO_DESC" + ',';
                } else if (index >= len-3) {
                    result_str += col + ',';
                }
            });

            result_str += "1";
            result_str = result_str.replaceAll('\n', '');
            result_str = result_str.replaceAll('\r', '');
            datas.push(result_str);
          
        });
  
        return datas;
      },
    }
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
  
  #menual {
    background-color: cadetblue;
    border: 1px solid black;
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
  