<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=viewport, initial-scale=1.0">
    <title>Table</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
 <style>
 

table, tr, td, th {
    border-collapse: collapse;
    border: 1px solid black;
    padding: 0.4rem;
    cursor: pointer;
}

th {
    width: 350px;
}

td {
    text-align: left;
}
        
 </style>
    <table id="cities-table">
        <thead>
            <tr>
                <th>City</th>
                <th>Population <span></span></th>
            </tr>
        </thead>
        <tbody>
        </tbody>
    </table>

<script>
     let citiesData = [
    { name: 'City A', population: 1000000, order: 'A' },
    { name: 'City B', population: 500000, order: 'B' },
    { name: 'City C', population: 750000, order: 'C' },
    { name: 'City D', population: 1200000, order: 'D' },
    { name: 'City E', population: 300000, order: 'E' },
];
let isAscendingOrder = true;
let clickCount = 0;
function displayCities() {
    const tableBody = document.querySelector('#cities-table tbody');
    tableBody.innerHTML = ''; 
    for (let i = 0; i < citiesData.length; i++) {
        const city = citiesData[i];
        const row = document.createElement('tr');
        row.innerHTML = '<td>' + city.name + '</td><td>' + city.population + '</td>';
        tableBody.appendChild(row);
    }
}
function sortCities(column) {
    const populationHeader = document.querySelector('#cities-table th:nth-child(2) span');
    clickCount++;
    if (clickCount === 1) {  
        if (column === 'population') {
            citiesData.sort(function (a, b) {
                return a.population - b.population;
            });
        } else {
            citiesData.sort(function (a, b) {
                return a.order.localeCompare(b.order);
            });
        }
        populationHeader.textContent = ' ▲'; 
    } else if (clickCount === 2) {
        if (column === 'population') {
            citiesData.sort(function (a, b) {
                return b.population - a.population;
            });
        } else {
            citiesData.sort(function (a, b) {
                return b.order.localeCompare(a.order);
            });
        }
        populationHeader.textContent = ' ▼'; 
    } else {
        citiesData.sort(function (a, b) {
            return a.order.localeCompare(b.order);
        });
        populationHeader.textContent = ''; 
        clickCount = 0; 
    }
    displayCities();
}
displayCities();
document.querySelector('#cities-table th:first-child').addEventListener('click', function () {
    sortCities('name');
});
document.querySelector('#cities-table th:nth-child(2)').addEventListener('click', function () {
    sortCities('population');
});

</script>
</body>
</html>
