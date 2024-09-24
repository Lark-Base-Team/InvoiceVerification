<template>
  <div class="center">
    <el-link href="https://dac57ho49r5.feishu.cn/docx/MG5KdjT5lo5fTOxLoNBcRIFTnYc" target="_blank">
      <el-text tag="b">{{ $t('form.appCode') }}</el-text>
    </el-link>

    <el-text>{{ $t('form.feishuDocument') }}</el-text>

    <el-link href="https://bytedance.larkoffice.com/docx/WXtGdRmOioeH9VxlfCtc1Y41nKe" target="_blank">
      <el-text tag="b">{{ $t('form.plugIn') }}</el-text>
    </el-link>

    <el-text class="mt-10">{{ $t('form.defaultcode') }}</el-text>

    <el-skeleton class="skeleton" :loading="appcodeLoading" animated>
      <template #template>
        <el-skeleton-item class="skeleton-item" />
      </template>
      <template #default>
        <el-text>{{ defaultAppCode }}</el-text>
      </template>
    </el-skeleton>

    <el-text>{{ $t('form.remain') }}</el-text>

    <el-skeleton class="skeleton" :loading="remainLoading" animated>
      <template #template>
        <el-skeleton-item class="skeleton-item-small" />
      </template>
      <template #default>
        <el-text>{{ remain }}</el-text>
      </template>
    </el-skeleton>

    <el-input class="mt-5" v-model="input" type="password" :placeholder="$t('form.enterAppcode')" show-password />

    <div class="full-width flex-row">
      <el-popover width="200px" placement="top-start" :title="$t('form.content.unneccessary')" :width="400"
        trigger="hover" :content="$t('form.content.fpdmRemind')">
        <template #reference>
          <el-text class="mt-20" size="default">{{ $t('form.content.fpdmTitle') }}</el-text>
        </template>
      </el-popover>
    </div>
    <el-select class="full-width mt-5" v-model="fpdmContent" :placeholder="$t('form.content.textSelect')" size="large"
      :no-data-text="$t('form.content.noField')">
      <el-option v-for="item in fieldList" :key="item.id" :value="item.name" @click="renewField('fpdm', item)" />
    </el-select>

    <div class="full-width flex-row">
      <el-popover width="200px" placement="top-start" :title="$t('form.content.neccessary')" :width="400"
        trigger="hover" :content="$t('form.content.fphmRemind')">
        <template #reference>
          <el-text class="mt-20" size="default">{{ $t('form.content.fphmTitle') }}</el-text>
        </template>
      </el-popover>
    </div>
    <el-select class="full-width mt-5" v-model="fphmContent" :placeholder="$t('form.content.textSelect')" size="large"
      :no-data-text="$t('form.content.noField')">
      <el-option v-for="item in fieldList" :key="item.id" :value="item.name" @click="renewField('fphm', item)" />
    </el-select>

    <div class="full-width flex-row">
      <el-popover width="200px" placement="top-start" :title="$t('form.content.unneccessary')" :width="400"
        trigger="hover" :content="$t('form.content.xymRemind')">
        <template #reference>
          <el-text class="mt-20" size="default">{{ $t('form.content.xymTitle') }}</el-text>
        </template>
      </el-popover>
    </div>
    <el-select class="full-width mt-5" v-model="xymContent" :placeholder="$t('form.content.textSelect')" size="large"
      :no-data-text="$t('form.content.noField')">
      <el-option v-for="item in fieldList" :key="item.id" :value="item.name" @click="renewField('xym', item)" />
    </el-select>

    <div class="full-width flex-row">
      <el-popover width="200px" placement="top-start" :title="$t('form.content.neccessary')" :width="400"
        trigger="hover" :content="$t('form.content.kprqRemind')">
        <template #reference>
          <el-text class="mt-20" size="default">{{ $t('form.content.kprqTitle') }}</el-text>
        </template>
      </el-popover>
    </div>
    <el-select class="full-width mt-5" v-model="kprqContent" :placeholder="$t('form.content.dateSelect')" size="large"
      :no-data-text="$t('form.content.noField')">
      <el-option v-for="item in fieldList" :key="item.id" :value="item.name" @click="renewField('kprq', item)" />
    </el-select>

    <div class="full-width flex-row">
      <el-popover width="200px" placement="top-start" :title="$t('form.content.unneccessary')" :width="400"
        trigger="hover" :content="$t('form.content.bhsjeRemind')">
        <template #reference>
          <el-text class="mt-20" size="default">{{ $t('form.content.bhsjeTitle') }}</el-text>
        </template>
      </el-popover>
    </div>
    <el-select class="full-width mt-5" v-model="bhsjeContent" :placeholder="$t('form.content.moneySelect')" size="large"
      :no-data-text="$t('form.content.noField')">
      <el-option v-for="item in fieldList" :key="item.id" :value="item.name" @click="renewField('bhsje', item)" />
    </el-select>

    <el-text class="full-width mt-20" size="default">{{ $t('form.content.yzTitle') }}</el-text>
    <el-select class="full-width mt-5" v-model="yzContent" :placeholder="$t('form.content.pleaseSelect')" size="large"
      :no-data-text="$t('form.content.noField')">
      <el-option v-for="item in fieldList" :key="item.id" :value="item.name" @click="renewField('yz', item)" />
    </el-select>

    <el-text class="full-width mt-20" size="default">{{ $t('form.content.zfTitle') }}</el-text>
    <el-select class="full-width mt-5" v-model="zfContent" :placeholder="$t('form.content.pleaseSelect')" size="large"
      :no-data-text="$t('form.content.noField')">
      <el-option v-for="item in fieldList" :key="item.id" :value="item.name" @click="renewField('zf', item)" />
    </el-select>

    <el-text class="full-width mt-20" size="default">{{ $t('form.content.chTitle') }}</el-text>
    <el-select class="full-width mt-5" v-model="chContent" :placeholder="$t('form.content.pleaseSelect')" size="large"
      :no-data-text="$t('form.content.noField')">
      <el-option v-for="item in fieldList" :key="item.id" :value="item.name" @click="renewField('ch', item)" />
    </el-select>

    <el-button type="primary" class="full-width mt-23" :disabled="able" @click="submitData">{{ $t('form.content.submit')
      }}</el-button>
  </div>
</template>


<script setup>

import { ref, onMounted, h, watch } from 'vue';
import { bitable } from '@lark-base-open/js-sdk';
import axios from 'axios';
import { ElLoading, ElMessage, ElNotification } from 'element-plus';
import { useI18n } from 'vue-i18n';
import { useStorage } from '@vueuse/core'


let locale = 'zh'
let fieldList = ref([])
let submitList = []
const storageVariables = {};
const selection = ref({})
const records = ref([])
const remain = ref('获取中')
const defaultAppCode = ref('获取中')
const appcodeLoading = ref(true)
const remainLoading = ref(true)
const able = ref(false)


const fields = ['fpdm', 'fphm', 'kprq', 'xym', 'bhsje', 'yz', 'zf', 'ch', 'appcode'];
const fieldIds = ['codeFieldId', 'numFieldId', 'checkFieldId', 'sumFieldId', 'dateFieldId', 'yzFieldId', 'zfFieldId', 'chFieldId', 'vid'];

fields.forEach(field => {
  const storageKey = field === 'appcode' ? 'input' : `${field}Content`;
  storageVariables[storageKey] = useStorage(storageKey, '');
});

fieldIds.forEach(fieldId => {
  const storageKey = fieldId === 'vid' ? 'viewId' : fieldId;
  storageVariables[storageKey] = useStorage(storageKey, '');
});

const {
  fpdmContent, fphmContent, kprqContent, xymContent, bhsjeContent, yzContent, zfContent, chContent,
  input, codeFieldId, numFieldId, checkFieldId, sumFieldId, dateFieldId, yzFieldId, zfFieldId, chFieldId, viewId
} = storageVariables;


const fieldsMapping = {
  fpdm: { content: 'fpdmContent', id: 'codeFieldId' },
  fphm: { content: 'fphmContent', id: 'numFieldId' },
  xym: { content: 'xymContent', id: 'checkFieldId' },
  kprq: { content: 'kprqContent', id: 'dateFieldId' },
  bhsje: { content: 'bhsjeContent', id: 'sumFieldId' },
  yz: { content: 'yzContent', id: 'yzFieldId' },
  zf: { content: 'zfContent', id: 'zfFieldId' },
  ch: { content: 'chContent', id: 'chFieldId' }
};

const renewField = (fieldKey, item) => {
  const { content, id } = fieldsMapping[fieldKey];
  storageVariables[content].value = item.name;
  storageVariables[id].value = item.id;
};

const showMessage = (type, messageZh, messageEn, additionalInfo = '') => {
  const message = locale == 'zh' ? messageZh + additionalInfo : messageEn + additionalInfo;
  ElMessage({
    message,
    type,
  });
};

const showError = (e, messageZh, messageEn) => {
  const message = locale == 'zh'
    ? `${messageZh}${e.num}获取数据失败(${e.message})`
    : `${messageEn}${e.num}failed to obtain data(${e.message})`;
  ElMessage.error(message);
};

const showNotification = (titleZh, titleEn, messageZh, messageEn) => {
  const title = locale == 'zh' ? titleZh : titleEn;
  const message = locale == 'zh'
    ? h('i', { style: 'color: black' }, messageZh)
    : h('i', { style: 'color: black' }, messageEn);
  ElNotification({
    title,
    message,
  });
};


onMounted(async () => {
  fetchRemain();
  useI18n();
  locale = await bitable.bridge.getLanguage()
  bitable.base.onSelectionChange(() => {
    reloadData()
  })
  reloadData()
})

watch([defaultAppCode, remain], ([newDefaultAppCode, newRemain]) => {
  if (newDefaultAppCode !== undefined) {
    appcodeLoading.value = false;
  }
  if (newRemain !== undefined) {
    remainLoading.value = false;
  }
});

const fetchRemain = () => {
  axios.get('https://47.121.132.8/')
    .then((res) => {
      remain.value = res.data.rest
      defaultAppCode.value = res.data.appcode
    })
    .catch((err) => {
      remain.value = 0
      defaultAppCode.value = err.data.message
    })
}

const resetFields = () => {
  const fields = [
    'codeFieldId', 'numFieldId', 'checkFieldId', 'sumFieldId',
    'dateFieldId', 'yzFieldId', 'zfFieldId', 'chFieldId',
    'fpdmContent', 'fphmContent', 'kprqContent', 'xymContent',
    'bhsjeContent', 'yzContent', 'zfContent', 'chContent'
  ];
  fields.forEach(field => storageVariables[field].value = '');
};


const reloadData = async () => {
  selection.value = await bitable.base.getSelection();
  if (viewId.value != selection.value.viewId) {
    viewId.value = selection.value.viewId
    resetFields();
  }
  const table = await bitable.base.getTableById(selection.value.tableId)
  const view = await table.getViewById(selection.value.viewId);
  const fieldListId = await view.getVisibleFieldIdList()
  fieldList.value = []
  for (let element of fieldListId) {
    let fmeta = await table.getFieldMetaById(element)
    let newEle = {
      id: fmeta.id,
      name: fmeta.name
    }
    fieldList.value = fieldList.value.concat(newEle)
  }
  console.log(selection.value)
  let recordIdData;
  let token;
  const loadingParams = {
    lock: true,
    text: 'Loading',
    background: 'rgba(0, 0, 0, 0.7)',
  }
  let loadingService = ElLoading.service(loadingParams)
  records.value = []
  do {
    recordIdData = await view.getVisibleRecordIdListByPage(token ? { pageToken: token, pageSize: 200 } : { pageSize: 200 });
    token = recordIdData.pageToken
    loadingService.setText(`${((token > 200 ? (token - 200) : 0) / recordIdData.total * 100).toFixed(2)}%`)
    records.value.push(...recordIdData.recordIds);
  } while (recordIdData.hasMore);
  loadingService.close()
  console.log(records.value);

}

const submitData = async () => {
  if (input.value == '') {
    showNotification('提示', 'Prompt', '请填写AppCode', 'Please fill in AppCode');
  } else if (fpdmContent.value != '' && fphmContent.value != '' && kprqContent.value != '' && xymContent.value != '' && bhsjeContent.value != '' && yzContent.value != '' && zfContent.value != '' && chContent.value != '') {
    able.value = true
    const table = await bitable.base.getTableById(selection.value.tableId);
    const [codeField, numField, checkField, sumField, dateField, yzField, chField, zfField] = await Promise.all([
      table.getField(codeFieldId.value), table.getField(numFieldId.value), table.getField(checkFieldId.value), table.getField(sumFieldId.value),
      table.getField(dateFieldId.value), table.getField(yzFieldId.value), table.getField(chFieldId.value), table.getField(zfFieldId.value)
    ]);

    for (let record of records.value) {
      const getCellValue = async (field, record) => {
        const cell = await field.getCell(record);
        return await cell.getValue();
      };
      const [yzRes, chRes, zfRes] = await Promise.all([
        getCellValue(yzField, record),
        getCellValue(chField, record),
        getCellValue(zfField, record)
      ]);
      if (yzRes == null && chRes == null && zfRes == null) {
        const getValueAndFormat = async (field, record, formatter) => {
          const cell = await field.getCell(record);
          const res = await cell.getValue();
          if (res != null) {
            return formatter(res);
          }
          return '';
        };
        const formatDate = (date) => {
          if (typeof date == 'number') {
            const newDate = new Date(date);
            const Y = newDate.getFullYear();
            const M = (newDate.getMonth() + 1 < 10 ? '0' + (newDate.getMonth() + 1) : newDate.getMonth() + 1);
            const D = (newDate.getDate() < 10 ? '0' + newDate.getDate() : newDate.getDate());
            return '' + Y + M + D;
          } else {
            return date[0].text.split('').filter(letter => !Number.isNaN(parseInt(letter))).join('');
          }
        };
        const [codeVal, numVal, checkVal, sumVal, dateVal] = await Promise.all([
          getValueAndFormat(codeField, record, (res) => res != null ? res[0].text : ''),
          getValueAndFormat(numField, record, (res) => res != null ? res[0].text : ''),
          getValueAndFormat(checkField, record, (res) => res != null ? res[0].text : ''),
          getValueAndFormat(sumField, record, (res) => typeof res == 'number' ? '' + res : res[0].text.split('').filter(letter => !Number.isNaN(parseInt(letter)) || letter == '.').join('')),
          getValueAndFormat(dateField, record, formatDate)
        ]);
        let submit = { recordId: record, codeVal, numVal, checkVal, sumVal, dateVal }
        submitList = submitList.concat(submit)
      }
    }
    await requestData()
  } else {
    showNotification('提示', 'Prompt', '请完整填写列表', 'Please fill out the complete list');
  }
}

const requestData = async () => {
  const table = await bitable.base.getTableById(selection.value.tableId);
  for (let record of submitList) {
    try {
      const response = await axios.post('https://jminvoice.market.alicloudapi.com/invoice/validate', {
        fpdm: record.codeVal,
        fphm: record.numVal,
        kprq: record.dateVal,
        bhsje: record.sumVal,
        xym: record.checkVal
      }, {
        headers: {
          'Content-Type': 'application/x-www-form-urlencoded; charset=UTF-8',
          'Authorization': `APPCODE ${input.value}`
        }
      });
      let message, cancellationMark, hcbz;
      if (response.data.data.message === '一致') {
        const { invoiceNo, cancellationMark: cancelMark, hcbz: hcbzVal } = response.data.data.info;
        showMessage('success', `发票号码${invoiceNo}核验正确`, `Invoice number ${invoiceNo} verified to be correct`);
        const messages = {
          'zh': { consistent: '一致', notVoided: '未作废', voided: '已作废', unredOffset: '未红冲', fullRedOffset: '全额红冲', partialRedOffset: '部分红冲' },
          'en': { consistent: 'Consistent', notVoided: 'Not Voided', voided: 'Voided', unredOffset: 'Unred Offset', fullRedOffset: 'Full Red Offset', partialRedOffset: 'Partial Red Offset' }
        };
        const localeMessages = messages[locale];
        message = localeMessages.consistent;
        cancellationMark = cancelMark === '0' ? localeMessages.notVoided : localeMessages.voided;
        const hcbzMap = {
          '0': localeMessages.unredOffset,
          '1': localeMessages.fullRedOffset,
          '2': localeMessages.partialRedOffset
        };
        hcbz = hcbzMap[hcbzVal];
      } else if (response.data.data.message === '不一致') {
        showMessage('warning', `发票号码${record.numVal}核验错误`, `Invoice number ${record.numVal} verified to be wrong`);
        message = locale === 'zh' ? '不一致' : 'Inconsistent';
      }
      await Promise.all([
        table.setCellValue(yzFieldId.value, record.recordId, message),
        table.setCellValue(zfFieldId.value, record.recordId, cancellationMark),
        table.setCellValue(chFieldId.value, record.recordId, hcbz)
      ]);
    } catch (error) {
      const message = locale === 'zh' ? '参数错误' : 'Parameter error';
      showError({ message, num: record.numVal }, '发票号码', 'Invoice number');
      await table.setCellValue(yzFieldId.value, record.recordId, message);
    }
  }
};

</script>

<style scoped>
.center {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  ;
}

.mt-10 {
  margin-top: 10px;
}

.mt-5 {
  margin-top: 5px;
}

.mt-20 {
  margin-top: 20px;
}

.mt-23 {
  margin-top: 23px;
}

.full-width {
  width: 100%;
}

.flex-row {
  display: flex;
  flex-direction: row;
}

.skeleton {
  display: flex;
  justify-content: center;
}

.skeleton-item {
  width: 80%;
  height: 20px;
}

.skeleton-item-small {
  width: 15%;
  height: 20px;
}
</style>
