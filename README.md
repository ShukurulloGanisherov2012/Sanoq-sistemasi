create  components papka

CountryDetail :


import React, { useEffect, useState } from 'react';
import { useParams } from 'react-router-dom';

function CountryDetail() {
    const { name } = useParams();
    const [country, setCountry] = useState();

    useEffect(() => {
        fetch(`https://restcountries.com/v3.1/name/${name}`)
            .then(res => res.json())
            .then(data => setCountry(data[0]))
            .catch(error => console.error('Error fetching country:', error));
    }, [name]);

    if (!country) {
        return <div>Yuklanmoqda...</div>;
    }

    return (
        <div className='detailCard'>
            <img className='img' src={country.flags ? country.flags.png : ''} alt={country.name ? `${country.name.common} flag` : 'Flag'} />
            <div className="txt">
                <h1 style={{fontSize: "45px"}}>{country.name ? country.name.common : 'N/A'}</h1>
                <p style={{fontSize: "25px"}}><b>Population:</b> {country.population ? country.population.toLocaleString() : 'N/A'}</p>
                <p style={{fontSize: "25px"}}><b>Region:</b> {country.region ? country.region : 'N/A'}</p>
                <p style={{fontSize: "25px"}}><b>Capital:</b> {country.capital ? country.capital[0] : 'N/A'}</p>
                <p style={{fontSize: "25px"}}><b>Subregion:</b> {country.subregion ? country.subregion : 'N/A'}</p>
                <p style={{fontSize: "25px"}}><b>Languages:</b> {country.languages ? Object.values(country.languages).join(', ') : 'N/A'}</p>
            </div>
        </div>
    );
}

export default CountryDetail;



Countries.jsx:
import React, { useEffect, useState } from 'react';
import { Link } from 'react-router-dom';

export default function Countries() {
    const [countries, setCountries] = useState([]);

    useEffect(() => {
        fetch('https://restcountries.com/v3.1/all')
            .then(res => res.json())
            .then(data => setCountries(data));
    }, []);

    return (
        <div>
            <h1>Countries</h1>
            <div className="country-list">
                {countries.map(country => (
                    <Link to={`/country/${country.name.common}`} key={country.cca3} className="card">
                        <img src={country.flags.png} alt={`${country.name.common} flag`} />
                        <div className="card-text">
                            <h3>{country.name.common}</h3>
                            <p><b>Population:</b> {country.population.toLocaleString()}</p>
                            <p><b>Region:</b> {country.region}</p>
                            <p><b>Capital:</b> {country.capital ? country.capital[0] : 'N/A'}</p>
                        </div>
                    </Link>
                ))}
            </div>
        </div>
    );







App.css 

/* src/App.css */
.App {
    font-family: Arial, sans-serif;
    padding: 20px;
}
*{
    font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
}

.country-list {
    display: flex;
    flex-wrap: wrap;
    width: 100%;
    justify-content: space-between;
    gap: 30px;
}

.card {
    background: white;
    border: 1px solid #ddd;
    padding: 10px;
    width: 300px;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    border-radius: 8px;
    text-align: center;
    text-decoration: none;
    color: inherit;
    transition: all .4s ease;
}
.card:hover{
    transform: scale(1.1);
}

.card img {
    width: 100%;
    height: 200px;
    border-radius: 8px;
    box-shadow: 0.5px 0.5px 5px 0.1px gray;
}

.card-text {
    padding: 10px;
}
.detailCard{
    display: flex;
    width: 1200px;
    margin: 200px auto;
    gap: 30px;
}
.img{
    width: 730px;
    height: 400px;
    box-shadow: 0.5px 0.5px 5px 0.1px gray;
    border-radius: 8px;
}


}








main.jsx


import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.jsx'
import './index.css'

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
)

