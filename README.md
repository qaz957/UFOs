# UFO Sightings

## Overview
Create a website using Java and HTML to collet and visualize UFO sightings accross the US with filterable results.

## Analysis

### Code

We used multiple functions to parse and filter the data given to us.

- First we built the table

      function buildTable(data) {
        tbody.html("");

        data.forEach((dataRow) => {
          let row = tbody.append("tr");
          Object.values(dataRow).forEach((val) => {
            
            let cell = row.append("td");
            cell.text(val);
          });
        });
      }
      
- Then we made a function with an if/else statement to update the filters we were using on the data

      // Use this function to update the filters. 
      function updateFilters() {

          // Save the element that was changed as a variable.
            let element = d3.select(this);

          // Save the value that was changed as a variable.
            let elementValue = element.property("value");
            console.log(elementValue); 

          // Save the id of the filter that was changed as a variable.
            let filterId = element.attr("id");
            console.log(filterId);

          // If a filter value was entered then add that filterId and value
          // to the filters list. Otherwise, clear that filter from the filters object.
          if (elementValue) {
            filters[filterId]=elementValue;
          }
          else {
            delete filters[filterId];
          }

          // Call function to apply all filters and rebuild the table
          filterTable();
        }
      
 - We wrote another function to filter the data in the table and at the end called the function to populate it

       // Use this function to filter the table when data is entered.
        function filterTable() {

          // Set the filtered data to the tableData.
          let filteredData = tableData;

          // Loop through all of the filters and keep any data that
          // matches the filter values
          Object.entries(filters).forEach(([key, value]) => {
            filteredData = filteredData.filter(row => row[key] === value);
          });

          // Finally, rebuild the table using the filtered data
          buildTable(filteredData);
        }

        // Attach an event to listen for changes to each filter
        d3.selectAll("input").on("change", updateFilters);

        // Build the table when the page loads
        buildTable(tableData);
        
### Site

What we ended up with is a site that has multiple filters that allows the user the arranegt he data how they see fit by entering parameters into the input boxes on the left of the page.

![image](https://user-images.githubusercontent.com/108296899/193115918-0b37ef43-19c3-48df-8035-201c34a8ef95.png)

## Summary

While this is a good start. One drawback is that there is no limit to the values you can enter. This opens a lot of oppurtunity for errors resulting in empty data. We could use dropdown menus for some of the paramters such as "State" that would limit the user to only choosing existing values for the filters. Another possible improvement would be mapping the filtered results, but that would involve using a Maps API and that would probably go way beyond the scope of the project.


