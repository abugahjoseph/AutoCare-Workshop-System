# AutoCare-Workshop-System
Automotive Workshop Management System - Group Project
@bp.route("/vehicles/new/<int:customer_id>", methods=["GET", "POST"])
def new_vehicle(customer_id)
@bp.route("/vehicles/new/<int:customer_id>", methods=["GET", "POST"])
def new_vehicle(customer_id):
    customer = Customer.query.get_or_404(customer_id)

    if request.method == "POST":
        registration = request.form.get("registration", "").strip().upper()
        make = request.form.get("make", "").strip()
        model = request.form.get("model", "").strip()
        year_text = request.form.get("year", "").strip()

        if not registration or not make or not model:
            flash("Registration, make and model are required.", "danger")
        elif Vehicle.query.filter_by(registration=registration).first():
            flash("This vehicle registration number already exists.", "danger")
        else:
            try:
                year = int(year_text) if year_text else None
                if year is not None and not 1950 <= year <= 2035:
                    raise ValueError()

                vehicle = Vehicle(
                    registration=registration,
                    make=make,
                    model=model,
                    year=year,
                
    customer_id=customer.id
                )
                db.session.add(vehicle)
                db.session.commit()
                flash("Vehicle registered successfully.", "success")
                return redirect(url_for("main.index"))
            except ValueError:
                db.session.rollback()
                flash("Enter a valid vehicle year between 1950 and 2035.", "danger")

    return render_template("vehicle_form.html", customer=customer)

    
update Addo Kingsley_925:Add repair testing module
update Abdul Fatawu Qrwatu_926: Implement vehicle management
update Amankwah Jonas_923: Add customer registration feature
