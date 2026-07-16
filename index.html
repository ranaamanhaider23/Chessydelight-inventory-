import streamlit as st
import pandas as pd
import os

st.set_page_config(page_title="Cheesy Delights | Pro", layout="wide")

# --- DATA HELPERS ---
def load_data():
    menu_df = pd.read_csv("menu_data.csv") if os.path.exists("menu_data.csv") else pd.DataFrame(columns=["Item Name", "Current Stock"])
    bazar_df = pd.read_csv("bazar_data.csv") if os.path.exists("bazar_data.csv") else pd.DataFrame(columns=["Item Name", "Current Stock"])
    admin = open("admin.txt", "r").read().strip() if os.path.exists("admin.txt") else "Admin"
    pwd = open("password.txt", "r").read().strip() if os.path.exists("password.txt") else "1234"
    return menu_df, bazar_df, admin, pwd

def save_data(m, b):
    m.to_csv("menu_data.csv", index=False)
    b.to_csv("bazar_data.csv", index=False)

menu_db, bazar_db, admin_name, admin_pass = load_data()

# --- LOGIN ---
if "logged_in" not in st.session_state: st.session_state.logged_in = False
if not st.session_state.logged_in:
    st.title("🔐 Admin Login")
    with st.form("login_form"):
        u = st.text_input("Admin Name")
        p = st.text_input("Password", type="password")
        if st.form_submit_button("Login"):
            if u == admin_name and p == admin_pass:
                st.session_state.logged_in = True
                st.rerun()
            else: st.error("Wrong Details!")
    st.stop()

# --- FUNCTIONS ---
def render_inventory(df, db_name):
    search = st.text_input(f"🔍 Search {db_name}...", key=f"s_{db_name}")
    filtered = df[df["Item Name"].astype(str).str.contains(search, case=False, na=False)]
    
    for i, row in filtered.iterrows():
        with st.container(border=True):
            col1, col2, col3 = st.columns([2, 2, 2])
            col1.metric(str(row['Item Name']), value=row['Current Stock'])
            
            with col2:
                add_val = st.number_input("Add Qty", min_value=0, key=f"add_{db_name}_{i}")
                if st.button("➕ Add", key=f"btn_add_{db_name}_{i}"):
                    df.at[i, "Current Stock"] += add_val
                    save_data(menu_db, bazar_db); st.rerun()
            with col3:
                sub_val = st.number_input("Use Qty", min_value=0, key=f"sub_{db_name}_{i}")
                if st.button("➖ Use", key=f"btn_sub_{db_name}_{i}"):
                    df.at[i, "Current Stock"] -= sub_val
                    save_data(menu_db, bazar_db); st.rerun()

# --- TABS ---
tab0, tab1, tab2, tab3 = st.tabs(["📊 Stock Status", "📋 Menu Manager", "🛒 Bazar Supply", "⚙️ Settings"])

with tab0:
    st.subheader("⚠️ Stock Alerts & Overview")
    combined = pd.concat([menu_db.assign(Type="Menu"), bazar_db.assign(Type="Bazar")])
    low_stock = combined[combined["Current Stock"] < 5]
    
    if not low_stock.empty:
        st.error("🚨 ALERT: These items are running low (below 5)!")
        st.dataframe(low_stock, use_container_width=True)
    else:
        st.success("✅ All stocks are sufficient!")
        
    st.write("### Total Inventory")
    st.dataframe(combined, use_container_width=True)

with tab1:
    with st.form("new_menu"):
        n = st.text_input("New Item Name")
        if st.form_submit_button("Add New Item"):
            new_row = pd.DataFrame([[n, 0]], columns=["Item Name", "Current Stock"])
            menu_db = pd.concat([menu_db, new_row], ignore_index=True)
            save_data(menu_db, bazar_db); st.rerun()
    render_inventory(menu_db, "Menu")

with tab2:
    with st.form("new_bazar"):
        n = st.text_input("New Material Name")
        if st.form_submit_button("Add Material"):
            new_row = pd.DataFrame([[n, 0]], columns=["Item Name", "Current Stock"])
            bazar_db = pd.concat([bazar_db, new_row], ignore_index=True)
            save_data(menu_db, bazar_db); st.rerun()
    render_inventory(bazar_db, "Bazar")

with tab3:
    st.subheader("⚙️ Settings")
    col1, col2 = st.columns(2)
    with col1:
        del_m = st.selectbox("Delete from Menu", menu_db["Item Name"].tolist())
        if st.button("Confirm Delete Menu"):
            menu_db = menu_db[menu_db["Item Name"] != del_m]
            save_data(menu_db, bazar_db); st.rerun()
        
        del_b = st.selectbox("Delete from Bazar", bazar_db["Item Name"].tolist())
        if st.button("Confirm Delete Bazar"):
            bazar_db = bazar_db[bazar_db["Item Name"] != del_b]
            save_data(menu_db, bazar_db); st.rerun()

    with col2:
        with st.form("admin_settings"):
            new_admin = st.text_input("New Admin Name", value=admin_name)
            new_pass = st.text_input("New Password", type="password")
            if st.form_submit_button("Update Settings"):
                with open("admin.txt", "w") as f: f.write(new_admin)
                with open("password.txt", "w") as f: f.write(new_pass)
                st.success("Updated!"); st.rerun()
