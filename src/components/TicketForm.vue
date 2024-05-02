<template>
  <div>
    <form @submit.prevent="submitForm" v-if="!formSubmitted" class="form">
      <h2>Ticket Details</h2>

      <label for="category">Select a category</label><br>
      <select v-model="category" @change="updateTypeOptions" id="category" class="select">
        <option
          v-for="option in categories"
          :value="option"
          :key="option"
          :selected="option === category"
        >{{ option }}</option>
      </select><br>

      <label for="type">Select type(s)</label><br>
      <select v-model="selectedType" id="type" class="select" @change="addSelectedType">
        <option
          v-for="option in typeOptions"
          :value="option"
          :key="option"
        >{{ option }}</option>
      </select><br>
      <div class="chips">
        <div v-for="(chip, index) in selectedTypes" :key="index" class="chip">
          {{ chip }}
          <button @click.prevent="removeSelectedType(index)" class="remove-chip">×</button>
        </div>
      </div><br>

      <label for="subject">Subject</label><br>
      <input 
        v-model="subject"
        type="text"
        id="subject"
        placeholder=""
        required
        class="input"
      /><br>

      <label for="description">Description</label><br>
      <textarea 
        v-model="description"
        id="description"
        placeholder=""
        rows="4"
        required
        class="textarea"
      ></textarea><br>

      <div v-if="fileName" class="file-name">{{ fileName }}</div>

      <button class="add-file"  @click.prevent="addFile">
        Attach file
      </button><br>

      <div class="buttons">
        <input 
          class="cancel" 
          type="button" 
          value="Cancel"
          @click="cancelForm"
        >
        <input 
          class="submit" 
          type="submit" 
          value="Submit"
        >
      </div>
    </form>

    <div v-if="formSubmitted" class="submitted">
      <div class="submitted-content">
        <h3>Ticket Details</h3>
        <p><strong>Category:</strong> {{ category }}</p>
        <p><strong>Type(s):</strong></p>
        <ul>
          <li v-for="(type, index) in selectedTypes" :key="index">{{ type }}</li>
        </ul>
        <p><strong>Subject:</strong> {{ subject }}</p>
        <p><strong>Description:</strong> {{ description }}</p>
        <p><strong>Ticket Files & Documents:</strong> {{ fileName }}</p>
        <button @click="returnToForm" class="return-button">Return to Form</button>
      </div>
    </div>

  </div>
</template>

<script>
export default {
  data() {
    return {
      categories: ['Hardware', 'Software', 'Network', 'In-Processing'],
      typeOptions: [],
      selectedType: '',
      selectedTypes: [],
      subject: "",
      description: "",
      fileCount: 0,
      fileName: '',
      formSubmitted: false
    };
  },
  methods: {
    submitForm() {
      this.formSubmitted = true;
    },
    updateTypeOptions() {
      switch (this.category) {
        case 'Hardware':
          this.typeOptions = ['Laptop', 'Mobile', 'Peripherals', 'Desk Phone', 'Printers', 'Other'];
          break;
        case 'Software':
          this.typeOptions = ['Teams/Zoom', 'Mobile Blackberry', 'Adobe', 'Outlook', 'Microsoft Office', 'Other'];
          break;
        case 'Network':
          this.typeOptions = ['Network Access', 'Connectivity', 'VPN', 'Drivers', 'Other'];
          break;
        case 'In-Processing':
          this.typeOptions = ['Access Badge', 'Common Access Card (CAC)', 'SIPR', 'Trello'];
          break;
        default:
          this.typeOptions = [];
      }
    },
    addSelectedType() {
      if (this.selectedType !== '' && !this.selectedTypes.includes(this.selectedType)) {
        this.selectedTypes.push(this.selectedType);
        this.selectedType = '';
      }
    },
    removeSelectedType(index) {
      this.selectedTypes.splice(index, 1);
    },
    addFile() {
      this.fileCount++;
      this.fileName = `nameOfFileAttached${this.fileCount}.ext`;
    },
    cancelForm() {
      this.selectedType = ''; 
      this.selectedTypes = []; 
      this.subject = ''; 
      this.description = ''; 
      this.fileCount = 0;
      this.fileName = '';
    },
    returnToForm() {
      this.formSubmitted = false;
      this.cancelForm();
    }
  }
};
</script>

<style scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.form {
  width: 400px;
  padding: 20px;
  border: 2px solid #ccc;
  border-radius: 10px;
}

.select,
.input,
.textarea {
  width: calc(100% - 20px);
  padding: 8px;
  margin-bottom: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.chips {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.remove-chip {
  margin-left: 4px;
  background: none;
  border: none;
  cursor: pointer;
  color: #666;
}

.buttons {
  display: flex;
  justify-content: flex-end ;
  align-items: center;
}

.cancel {
  padding: 10px;
  background-color: grey;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.submit {
  padding: 10px;
  margin-left: 3px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}


.submitted {
  background-color: #f9f9f9;
  border: 2px solid #ccc;
  border-radius: 10px;
  padding: 20px;
  margin-top: 20px;
}

.submitted-content {
  max-width: 600px;
  margin: 0 auto;
}

.submitted h3 {
  margin-bottom: 10px;
}

.submitted ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

.submitted ul li {
  margin-bottom: 5px;
}

.add-file {
  padding: 10px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  margin-bottom: 10px;
}

.file-name {
  margin-bottom: 10px;
  font-weight: bold;
}

.return-button {
  padding: 10px;
  background-color: grey;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  margin-top: 20px;
}
</style>