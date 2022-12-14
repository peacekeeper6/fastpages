---
toc: true
layout: post
description: Formatted Rapid API
categories: [Habits]
image: images/tools.png
title: Rapid API Formatted
---

<table>
  <thead>
  <tr>
    <th>Song Name</th>
    <th>Artist</th>
    <th>Image Link</th>
    <th>Award</th>
  </tr>
  </thead>
  <tbody id="result">
    <!-- generated rows -->
  </tbody>
</table>

<!-- Script is layed out in a sequence (no function) and will execute when page is loaded -->
<script>
  // prepare HTML result container for new output
  const resultContainer = document.getElementById("result");

  // prepare fetch options
  const url = "https://billboard3.p.rapidapi.com/hot-100?date=2022-07-07&range=1-10";

  const options = {
	method: 'GET',
	headers: {
		'X-RapidAPI-Key': '9e4650470emshc2461cc01c07b29p18b9b5jsnfa759ab87fca',
		'X-RapidAPI-Host': 'billboard3.p.rapidapi.com'
	}
  };

  // fetch the API
  fetch(url, options)
    // response is a RESTful "promise" on any successful fetch
    .then(response => {
      // check for response errors
      if (response.status !== 200) {
          const errorMsg = 'Database response error: ' + response.status;
          console.log(errorMsg);
          const tr = document.createElement("tr");
          const td = document.createElement("td");
          td.innerHTML = errorMsg;
          tr.appendChild(td);
          resultContainer.appendChild(tr);
          return;
      }
      // valid response will have json data
      response.json().then(data => {
          console.log(data);

          // Country data
          for (const row of data) {
            console.log(row);

            // tr for each row
            const tr = document.createElement("tr");
            // td for each column
            const title = document.createElement("td");
            const artist = document.createElement("td");
            const image = document.createElement("td");
            const award = document.createElement("td");

            // data is specific to the API
            title.innerHTML = row.title;
            artist.innerHTML = row.artist; 
            image.innerHTML = row.image; 
            award.innerHTML = row.award; 

            // this build td's into tr
            tr.appendChild(title);
            tr.appendChild(artist);
            tr.appendChild(image);
            tr.appendChild(award);

            // add HTML to container
            resultContainer.appendChild(tr);
          }
      })
  })
  // catch fetch errors (ie ACCESS to server blocked)
  .catch(err => {
    console.error(err);
    const tr = document.createElement("tr");
    const td = document.createElement("td");
    td.innerHTML = err;
    tr.appendChild(td);
    resultContainer.appendChild(tr);
  });
</script>