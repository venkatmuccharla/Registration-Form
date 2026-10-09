#Registration Form 

import { useState } from "react";
import "./App.css";

function App() {
  const [data, setData] = useState([]);
  const [name, setName] = useState("");
  const [age, setAge] = useState("");
  const [email, setEmail] = useState("");
  const [show, setShow] = useState(false);

  function submit(e) {
    e.preventDefault();
    setData([...data, { name, age, email }]);
    setName("");
    setAge("");
    setEmail("");
  }

  return (
    <div className="container">
      <div className="left">
        <button onClick={() => document.getElementById("name").focus()}>Add</button>
        <button onClick={() => setShow(true)}>Filter</button>
        <button onClick={() => setData([])}>Delete All</button>
      </div>

  <div className="right">
        <h2>Registration Form</h2>
        <form onSubmit={submit}>
          <input id="name" placeholder="Name" value={name} onChange={e => setName(e.target.value)} required />
          <input placeholder="Age" type="number" value={age} onChange={e => setAge(e.target.value)} required />
          <input placeholder="Email" type="email" value={email} onChange={e => setEmail(e.target.value)} required />
          <button>Submit</button>
        </form>

  <h3>Submitted Data</h3>
        {data.map((d, i) => (
          <p key={i}>{d.name} - {d.age} - {d.email}
            <button onClick={() => setData(data.filter((_, j) => i !== j))}>Delete</button>
          </p>
        ))}

  {show && <div className="filter">
          <div><h3>Age &lt; 18</h3>
            {data.filter(d => +d.age < 18).map((d, i) => <p key={i}>{d.name} - {d.age}</p>)}
          </div>
          <div><h3>Age &gt;= 18</h3>
            {data.filter(d => +d.age >= 18).map((d, i) => <p key={i}>{d.name} - {d.age}</p>)}
          </div>
        </div>}
      </div>
    </div>
  );
}

export default App;
