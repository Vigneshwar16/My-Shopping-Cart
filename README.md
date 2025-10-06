# My-Shopping-Cart
Front End Development

import axios from 'axios'
import React, { useEffect, useState } from 'react'
import Color from '../props/Color'

const Carts = () => {
    const [carts, setCarts] = useState([])

    useEffect(() => {
        axios
            .get("https://dummyjson.com/carts")
            .then((response) => {
                setCarts(response.data.carts)
            })
            .catch((err) => {
                console.log(err)
            })
    }, [])

    // ✅ simple functions for button actions
    const handleAddToCart = (product) => {
        alert(`🛒 Added "${product.title}" to cart!`)
    }

    const handleBuyNow = (product) => {
        alert(`💰 Proceeding to buy "${product.title}"...`)
    }

    // ✅ hover effect handlers
    const handleMouseOver = (e) => {
        e.currentTarget.style.transform = "scale(1.05)"
        e.currentTarget.style.transition = "0.5s ease"
        e.currentTarget.style.boxShadow = "0 4px 15px rgba(190, 165, 83, 1)"
        e.currentTarget.style.background = "rgba(190, 165, 83, 1)"
    }

    const handleMouseOut = (e) => {
        e.currentTarget.style.transform = "scale(1)"
        e.currentTarget.style.boxShadow = "none"
        e.currentTarget.style.backgroundColor = "white"
    }

    const handleChangeOver = (e) => {
        e.currentTarget.style.transform = "scale(1.05)"
        e.currentTarget.style.color = "brown"
    }
    
    const handleChangeOut = (e) => {
        e.currentTarget.style.transform = "scale(1)"
        e.currentTarget.style.color = "black"
    }

    return (
        <div className='' >
            <div className='row ' style={{ display: "flex", justifyContent: "space-around", background: "black" }}>
                <h1 className='mb-0' style={{ display: "flex", justifyContent: "center", backgroundColor: "lightblue", height: 70 }}>Shopping Cart 🛒</h1>
                <nav className="navbar navbar-expand-lg bg-body-tertiary">
                    <div className="container-fluid" style={{ paddingLeft: 10 }} >
                        <button className="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarTogglerDemo03" aria-controls="navbarTogglerDemo03" aria-expanded="false" aria-label="Toggle navigation">
                            <span className="navbar-toggler-icon"></span>
                        </button>
                        <a className="navbar-brand ms-3" href="#" onMouseOver={handleChangeOver} onMouseOut={handleChangeOut}>Navbar</a>
                        <div className="collapse navbar-collapse" id="navbarTogglerDemo03" >
                            <ul className="navbar-nav me-auto mb-2 mb-lg-0">
                                <li className="nav-item">
                                    <a className="nav-link active" aria-current="page" href="#" onMouseOver={handleChangeOver} onMouseOut={handleChangeOut}>Home</a>
                                </li>
                                <li className="nav-item">
                                    <a className="nav-link" href="#" onMouseOver={handleChangeOver} onMouseOut={handleChangeOut}>Link</a>
                                </li>
                                <li className="nav-item">
                                    <a className="nav-link disabled" aria-disabled="true" onMouseOver={handleChangeOver} onMouseOut={handleChangeOut}>Disabled</a>
                                </li>
                            </ul>
                            <ul className="navbar-nav justify-content-end flex-grow-1 pe-3" style={{ paddingRight: 40 }}>
                                <li className="nav-item dropdown">
                                    <a className="nav-link dropdown-toggle" href="#" role="button" data-bs-toggle="dropdown" aria-expanded="false">
                                        ▼
                                    </a>
                                    <ul className="dropdown-menu" style={{left:"auto",right:0}}>
                                        <li><a className="dropdown-item" href="#">Action</a></li>
                                        <li><a className="dropdown-item" href="#">Another action</a></li>
                                        <li><a className="dropdown-item" href="#">Something else here</a></li>
                                    </ul>
                                </li>
                            </ul>
                        </div>
                    </div>
                </nav>

                {carts.map((c, index) => {
                    const product = c.products[0]
                    return (
                        <div1
                            key={index}
                            className='card mt-5 d-flex'
                            style={{ width: 300, height: "auto", textAlign: "center", padding: 20, }}
                            onMouseOver={handleMouseOver}     //  hover animation
                            onMouseOut={handleMouseOut}       //  restore style

                        >
                            <h3 style={{ textAlign: "center" }}>{product.title}</h3>
                            <img src={product.thumbnail} alt="image" style={{ fill: "ActiveBorder" }} />
                            <div className='' style={{ display: "flex" }}>
                                <p className='' style={{ fontFamily: "revert-layer", color: "green", paddingTop: 5 }} >Extra {product.discountPercentage}% off</p>
                            </div>
                            <div className='' style={{ display: "flex" }}>
                                <h3 className='' style={{ paddingRight: 8, float: "value" }}>${product.price}</h3>
                                <h6 style={{ color: "grey", textDecoration: "line-through" }}>{product.discountedTotal}</h6>
                            </div>
                            <div className='' style={{ padding: 10, display: "flex", justifyContent: "space-between" }}>
                                <button
                                    className=''
                                    style={{ backgroundColor: "orange", border: "none", borderRadius: 1 }}
                                    onClick={() => handleAddToCart(product)} // ✅ added
                                >
                                    Add to Cart
                                </button>
                                <button
                                    className=''
                                    style={{ backgroundColor: "red", border: "none", borderRadius: 1 }}
                                    onClick={() => handleBuyNow(product)} // ✅ added
                                >
                                    Buy Now
                                </button>
                            </div>
                        </div1>
                    )
                })}
                <div style={{paddingTop:50}}>
                <footer class="footer" style={{textAlign:"center", paddingBottom:50,paddingTop:20,background:"rgba(22, 50, 71, 1)"}}>
                    <p style={{color:"rgba(143, 186, 213, 1)"}}> © 2023 My Company Name. All rights reserved.</p>
                    <nav>
                        <div style={{color:'white'}}>
                        <a href="/privacy-policy" style={{color:'white'}}>Privacy Policy</a> | 
                        <a href="/terms-of-service" style={{color:'white'}}> Terms of Service</a> | 
                        <a href="/contact" style={{color:'white'}}> Contact Us</a>
                        </div>
                    </nav>
                </footer>
                </div>
            </div>
        </div>
    )
}

export default Carts
