import streamlit as st
import requests

st.set_page_config(page_title="Dhan OCO Order", layout="wide")

st.title("🔁 Dhan OCO Order App")

st.markdown("Place OCO (One Cancels the Other) orders via Dhan API")

# Input Fields
client_id = st.text_input("📧 Client ID")
access_token = st.text_input("🔐 Access Token", type="password")
symbol = st.text_input("📈 Symbol (e.g. NSE:RELIANCE)")
exchange_segment = st.selectbox("📊 Exchange Segment", ["NSE", "BSE"])
transaction_type = st.selectbox("📥 Transaction Type", ["BUY", "SELL"])
quantity = st.number_input("📦 Quantity", min_value=1, step=1)
price = st.number_input("💰 Limit Price")
trigger_price = st.number_input("🎯 Trigger Price")
stop_loss_price = st.number_input("🛡️ Stop Loss Price")

if st.button("🚀 Place OCO Order"):
    if not all([client_id, access_token, symbol]):
        st.warning("Please fill in all required fields.")
    else:
        headers = {
            "access-token": access_token,
            "Content-Type": "application/json"
        }

        payload = {
            "transaction_type": transaction_type,
            "exchange_segment": exchange_segment,
            "product_type": "INTRADAY",
            "order_type": "LIMIT",
            "price": price,
            "quantity": quantity,
            "trigger_price": trigger_price,
            "stop_loss_price": stop_loss_price,
            "symbol": symbol,
            "validity": "DAY",
            "amo": False,
            "order_source": "API"
        }

        url = f"https://api.dhan.co/orders/oco?client_id={client_id}"
        response = requests.post(url, headers=headers, json=payload)

        if response.status_code == 200:
            st.success("✅ Order placed successfully!")
            st.json(response.json())
        else:
            st.error("❌ Failed to place order.")
            st.json(response.json())
