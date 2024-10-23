const api_key = '899022c631188258f524bde75e9b4818';
const base_url = 'https://api.openweathermap.org/data/2.5/weather';

let is_dark_mode = false;

const body_el = document.body;
const header_el = document.getElementsByTagName('header')[0];
const dark_mode_toggle = document.getElementById('dark-mode-icon');
const search_bar_el = document.getElementById('search-bar');
const condition_el = document.getElementsByClassName('condition-info')[0];
const degree_el = document.getElementById('degree');
const response_location_el = document.getElementsByClassName('location')[0];
const feels_like_el = document.getElementById('feels-like');
const humidity_el = document.getElementById('humidity');
const wind_el = document.getElementById('wind-speed');

function render_data(data) {
    const { main, weather, name, sys, wind } = data;
    condition_el.textContent = weather[0].description;
    degree_el.textContent = Math.floor(main.temp - 273.15);
    response_location_el.textContent = `${name}, ${sys.country}`;
    feels_like_el.textContent = Math.floor(main.feels_like - 273.15);
    humidity_el.textContent = main.humidity;
    wind_el.textContent = wind.speed;

    // Add animations
    condition_el.classList.add('fadeInUp');
    degree_el.classList.add('fadeInUp');
    response_location_el.classList.add('fadeInUp');
    feels_like_el.classList.add('fadeInUp');
    humidity_el.classList.add('fadeInUp');
    wind_el.classList.add('fadeInUp');

    // Remove animations after they end to allow for re-trigger
    setTimeout(() => {
        condition_el.classList.remove('fadeInUp');
        degree_el.classList.remove('fadeInUp');
        response_location_el.classList.remove('fadeInUp');
        feels_like_el.classList.remove('fadeInUp');
        humidity_el.classList.remove('fadeInUp');
        wind_el.classList.remove('fadeInUp');
    }, 1000);
}

function getWeatherData(location) {
    const url = `${base_url}?q=${location}&appid=${api_key}`;

    fetch(url)
        .then(response => {
            if (!response.ok) {
                throw new Error('Network response was not ok');
            }
            return response.json();
        })
        .then(data => {
            render_data(data);
        })
        .catch(error => {
            console.error('Error fetching data:', error);
        });
}

// Initial load with default location (Chennai) but display Kolkata in the search bar
getWeatherData('Chennai');

// Event listener for search bar input
search_bar_el.addEventListener('keydown', (e) => {
    if (e.key === 'Enter' || e.key === 'Return') {
        const location = search_bar_el.value.trim();
        if (location) {
            getWeatherData(location);
        }
    }
});

// Dark mode toggle functionality
dark_mode_toggle.addEventListener('click', () => {
    is_dark_mode = !is_dark_mode;

    const toggleDarkModeIcon = (is_dark_mode) => {
        if (is_dark_mode) {
            dark_mode_toggle.setAttribute('icon', 'fxemoji:whitesun');
        } else {
            dark_mode_toggle.setAttribute('icon', 'iconamoon:mode-dark-fill');
        }
    };

    body_el.classList.toggle('dark-mode');
    header_el.classList.toggle('header-dark-mode');

    toggleDarkModeIcon(is_dark_mode);
});
