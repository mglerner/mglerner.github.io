<!--
.. title: NonNewtonian Scientists
.. slug: nonnewtonian-scientists
.. date: 2018-02-04 02:10:56 UTC
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
-->

I've been working on developing an annotated syllabus for diversity/inclusion/decolonisation in Physics and Astronomy. You can see the results
[here](https://github.com/mglerner/IntroductoryPhysics), and this page makes it easy for you to contribute: research a scientist, fill out the fields below, click the link, and you'll get the text I need to add someone to the syllabus. You can either email it to me (mglerner@protonmail.com) or send me a PR. I'll gladly reformat them to fix any small mistakes, so don't let that stop you!

<!-- Thanks to -->
<!-- https://www.w3schools.com/js/tryit.asp?filename=tryjs_form_elements -->
<!-- for example javascript code -->

<form id="ScientistForm">
  The scientist's name:<br>
  <input type="text" name="Name" size="60"><br>
  Where this goes in a specific textbook. First, the textbook:
  <select name="Textbook">
      <option value="">None</option>
      <option value="Chabay and Sherwood, Matter and Interactions, 4th   Edition">Chabay and Sherwood, Matter and Interactions, 4th Edition</option>
      <option value="Knight, Physics for Scientists and Engineers: A Strategic Approach with Modern Physics, 3rd Edition">Knight, Physics for Scientists and Engineers: A Strategic Approach with Modern Physics, 3rd Edition</option>
      <option value="Knight, College Physics: A Strategic Approach, 2nd Edition">Knight, College Physics: A Strategic Approach, 2nd Edition</option>
  </select>
  <br>
  Now, where does this scientist go in this textbook, e.g. "Chapter 32, section 2" Fill in as much as you know, but feel free to leave parts out if you don't know them.<br>
  Chapter: <input type="number" name="Chapter" min="0" max="100" value="0">
  <br>
  Section: <input type="number" name="Section" min="0" max="100" value="0">
  <br>
  Do you know information about a second textbook? Let me know via email (mglerner@protonmail.com) or by editing the generated text before you send it to me!
  <br>
  Contributors: (you can put your name here if you'd like it to be public, or leave it out if not!) <br>
  <input type="text" name="Contributors" size="60"><br>
  Description of the scientist: <br>
  <textarea rows="10" cols="60" name="Description"></textarea><br>
  Sources: (please cite things via the APA style if possible, but I'll convert your citations if you'd rather just give me
  <i>something</i>). Include as many sources as you'd like here. <br>
  <textarea rows="3" cols="60" name="Sources"></textarea><br>
  Photo: please give me the URL of a photo of the scientist. I can
  make smaller versions, so don't worry about size. Feel free to include multiple URLs!<br>
  <textarea rows="3" cols="60" name="Photo"></textarea><br>

</form>
  
Click "Try it" to generate the combined text, then email me the
results (<mglerner@protonmail.com>) or send me a PR (again, 
the repository is [here](https://github.com/mglerner/IntroductoryPhysics))!


<button style="height:50px;width:100px" onclick="formatIt()">Try it</button>

<p id="ScientistResults" style="background-color:LightGray;"></p>

<script>
function formatIt() {
    var x = document.getElementById("ScientistForm");
    var text = "";
    var textbook = "#Textbook<br><br>";
    var i;
    for (i = 0; i < x.length ;i++) {
        if (x.elements[i].name == "Textbook") {
            textbook += x.elements[i].value;
        } else if (x.elements[i].name == "Chapter") {
            if (x.elements[i].value > 0) {
                textbook += ", Chapter " + x.elements[i].value;
            }
        } else if (x.elements[i].name == "Section") {
            if (x.elements[i].value > 0) {
                textbook += ", Section " + x.elements[i].value;
            }
        } else {
            text += "# " + x.elements[i].name + "<br>" + x.elements[i].value + "<br><br>";
        }
    }
    document.getElementById("ScientistResults").innerHTML = text + textbook;
}
</script>

