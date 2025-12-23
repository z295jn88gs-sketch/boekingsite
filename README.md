  {/* Packages Grid */}
  <section className="py-24 px-6 -mt-16">
    <div className="max-w-7xl mx-auto">
      <div className="grid lg:grid-cols-3 gap-8">
        {packages.map((pkg, index) => (
          <motion.div
            key={pkg.id}
            className={`relative rounded-3xl ${pkg.bgColor} border-2 ${pkg.borderColor} overflow-hidden`}
            initial=
            animate=
            transition=
          >
            {pkg.popular && (
              <div className="absolute top-0 left-0 right-0 bg-gradient-to-r from-[#d4a853] to-[#e07a5f] text-white text-center py-2 font-bold text-sm">
                MEEST GEKOZEN
              </div>
            )}
            
            <div className={`p-8 ${pkg.popular ? 'pt-14' : ''}`}>
              {/* Header */}
              <div className="flex gap-1 mb-3">
                {[...Array(pkg.stars)].map((_, i) => (
                  <Star key={i} className="h-5 w-5 fill-[#d4a853] text-[#d4a853]" />
                ))}
              </div>
              <h2 className="text-3xl font-bold text-[#1e3a5f] mb-1">{pkg.name}</h2>
              <p className="text-gray-500 mb-6">{pkg.tagline}</p>
              
              {/* Price */}
              <div className="mb-8">
                <span className="text-5xl font-bold text-[#1e3a5f]">€{pkg.price.toFixed(2).replace('.', ',')}</span>
                <span className="text-gray-500 ml-2">per persoon</span>
              </div>

              {/* Breakdown */}
              <div className="bg-white rounded-2xl p-5 mb-6 shadow-sm">
                <h4 className="font-semibold text-[#1e3a5f] mb-4 text-sm uppercase tracking-wide">Prijsopbouw</h4>
                <div className="space-y-3">
                  {pkg.breakdown.map((item, i) => (
                    <div key={i} className="flex justify-between text-sm">
                      <span className="text-gray-600">{item.item}</span>
                      <span className="font-medium text-[#1e3a5f]">€{item.price.toFixed(2).replace('.', ',')}</span>
                    </div>
                  ))}
                  <div className="border-t pt-3 flex justify-between font-bold">
                    <span className="text-[#1e3a5f]">Totaal</span>
                    <span className="text-[#1e3a5f]">€{pkg.price.toFixed(2).replace('.', ',')}</span>
                  </div>
                </div>
              </div>

              {/* Includes */}
              <div className="mb-8">
                <h4 className="font-semibold text-[#1e3a5f] mb-4 text-sm uppercase tracking-wide">Inbegrepen</h4>
                <ul className="space-y-3">
                  {pkg.includes.map((item, i) => (
                    <li key={i} className="flex items-start gap-3">
                      <div className="mt-0.5 h-5 w-5 rounded-full bg-green-100 flex items-center justify-center flex-shrink-0">
                        <Check className="h-3 w-3 text-green-600" />
                      </div>
                      <span className="text-gray-700">{item}</span>
                    </li>
                  ))}
                </ul>
              </div>

              {/* Book Button */}
              <Button 
                onClick={() => handleBook(pkg)}
                className={`w-full py-6 text-lg font-semibold rounded-xl bg-gradient-to-r ${pkg.color} hover:opacity-90 text-white`}
              >
                Boek {pkg.name}
              </Button>
            </div>
          </motion.div>
        ))}
      </div>
    </div>
  </section>

  {/* What's Included */}
  <section className="py-24 px-6 bg-white">
    <div className="max-w-7xl mx-auto">
      <motion.div 
        className="text-center mb-16"
        initial=
        whileInView=
        viewport=
      >
        <h2 className="text-4xl font-bold text-[#1e3a5f] mb-4">
          Wat krijg je bij elk pakket?
        </h2>
      </motion.div>

      <div className="grid md:grid-cols-3 gap-8">
        {[
          { icon: Plane, title: 'Retourvlucht', desc: 'Vlucht naar Bulgarije en terug naar Nederland' },
          { icon: Hotel, title: 'Accommodatie', desc: '9 nachten verblijf in hotels (kwaliteit per pakket)' },
          { icon: Bus, title: 'Vervoer', desc: 'Alle transfers tussen de 3 bestemmingen' }
        ].map((item, index) => (
          <motion.div
            key={item.title}
            className="text-center p-8 rounded-2xl bg-[#faf9f6]"
            initial=
            whileInView=
            transition=
            viewport=
          >
            <div className="inline-flex items-center justify-center w-16 h-16 rounded-2xl bg-[#1e3a5f] mb-6">
              <item.icon className="h-8 w-8 text-[#d4a853]" />
            </div>
            <h3 className="text-xl font-bold text-[#1e3a5f] mb-3">{item.title}</h3>
            <p className="text-gray-600">{item.desc}</p>
          </motion.div>
        ))}
      </div>
    </div>
  </section>

  {/* Booking Dialog */}
  <Dialog open={showBooking} onOpenChange={setShowBooking}>
    <DialogContent className="max-w-2xl max-h-[90vh] overflow-y-auto">
      <DialogHeader>
        <DialogTitle className="text-2xl font-bold text-[#1e3a5f]">
          Boek {selectedPackage?.name} Pakket
        </DialogTitle>
      </DialogHeader>
      {selectedPackage && (
        <BookingForm 
          selectedPackage={selectedPackage} 
          onClose={() => setShowBooking(false)} 
        />
      )}
    </DialogContent>
  </Dialog>
</div>   ); }
