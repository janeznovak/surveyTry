<template>
  <div class="container">
    <!-- If you want to hide survey, comment the lines below -->
    <h2>SurveyJS Library - a sample survey below</h2>
    <survey :survey="survey"></survey>
    <h2>Something</h2>
  </div>
</template>

<script>
import * as SurveyVue from "survey-vue";
import "bootstrap/dist/css/bootstrap.css";
var Survey = SurveyVue.Survey;
Survey.cssType = "bootstrap";

import * as widgets from "surveyjs-widgets";

import { init as customWidget } from "../components/customwidget";

// widgets.icheck(SurveyVue);
widgets.select2(SurveyVue);
widgets.inputmask(SurveyVue);
widgets.jquerybarrating(SurveyVue);
widgets.jqueryuidatepicker(SurveyVue);
widgets.nouislider(SurveyVue);
widgets.select2tagbox(SurveyVue);
widgets.sortablejs(SurveyVue);
widgets.ckeditor(SurveyVue);
widgets.autocomplete(SurveyVue);
widgets.bootstrapslider(SurveyVue);
customWidget(SurveyVue);

SurveyVue.Serializer.addProperty("question", "tag:number");
// Survey
//     .StylesManager
//     .applyTheme("modern"); returns an error


export default {
  components: {
    Survey
  },
  data() {
    var json = {
    showQuestionNumbers: "off",
    questions: [
        {
            type: "radiogroup",
            name: "haveKids",
            title: "Do you have a kid(s)?",
            isRequired: true,
            choices: [
                "Yes", "No"
            ],
            colCount: 0
        }, {
            type: "dropdown",
            name: "kids",
            title: "How many kids do you have",
            visibleIf: "{haveKids}='Yes'",
            isRequired: true,
            choices: [1, 2, 3, 4, 5]
        }, {
            type: "dropdown",
            name: "kid1Age",
            title: "The first kid age:",
            visibleIf: "{haveKids}='Yes' and {kids} >= 1",
            isRequired: true,
            "choicesMax": 18
        }, {
            type: "dropdown",
            name: "kid2Age",
            title: "The second kid age:",
            visibleIf: "{haveKids}='Yes' and {kids} >= 2",
            isRequired: true,
            startWithNewLine: false,
            "choicesMax": 18
        }, {
            type: "dropdown",
            name: "kid3Age",
            title: "The third kid age:",
            visibleIf: "{haveKids}='Yes' and {kids} >= 3",
            isRequired: true,
            startWithNewLine: false,
            "choicesMax": 18
        }, {
            type: "dropdown",
            name: "kid4Age",
            title: "The fourth kid age:",
            visibleIf: "{haveKids}='Yes' and {kids} >= 4",
            isRequired: true,
            startWithNewLine: false,
            "choicesMax": 18
        }, {
            type: "dropdown",
            name: "kid5Age",
            title: "The fifth kid age:",
            visibleIf: "{haveKids}='Yes' and {kids} >= 5",
            isRequired: true,
            startWithNewLine: false,
            "choicesMax": 18
        }
    ]
    };
    var model = new SurveyVue.Model(json);

    // for doing something, when the survey is completed, eg. logging the object and data of survey. You could do something like sending the survey to the
    // server and then do something with it(eg. putting it in the db).
    model.onComplete.add((sender) => {
      var object = sender;
      var data = sender.data;
      console.log(object, data.haveKids);
    })
    return {
      survey: model
    };
  },
};

// this.survey.oncomplete.add(function() {
//   // var something = sender;
//   // var sad = sender.data;
//   // console.log(something, sad);
// })
// this.survey.oncomplete.add(function(sender) {
//   var something = sender;
//   var data = sender.data;
//   console.log(something, data);
// })

</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
