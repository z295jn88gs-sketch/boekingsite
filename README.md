import React, { useState } from 'react';
import { motion } from 'framer-motion';
import { Star, Check, Plane, Hotel, Bus, MapPin, X } from 'lucide-react';
import { Button } from '@/components/ui/button';
import { Dialog, DialogContent, DialogHeader, DialogTitle } from '@/components/ui/dialog';
import BookingForm from '@/components/BookingForm';

export default function Packages() {
  const [selectedPackage, setSelectedPackage] = useState(null);
  const [showBooking, setShowBooking] = useState(false);

  const packages = [
    {
      id: 'basic',
      name: 'Basic',
      tagline: 'Goedkoopste pakket',
      stars: 3,
      price: 906.97,
      color: 'from-slate-500 to-slate-700',
      bgColor: 'bg-slate-50',
      borderColor: 'border-slate-200',
      description: '3 sterren hotels incl. 1 activiteit bij 2 van de bestemmingen',
      breakdown: [
        { item: 'Vlucht', price: 322.97 },
        { item: 'Hotels', price: 497.00 },
        { item: 'Vervoer', price: 69.00 },
        { item: 'Activiteit', price: 18.00 }
      ],
      includes: [
        'Vlucht heen en terug',
        '3★ hotels',
        'Vervoer tussen bestemmingen',
        '1 activiteit bij 2 bestemmingen'
      ]
    },
    {
      id: 'premium',
      name: 'Premium',
      tagline: 'Middenklasse pakket',
      stars: 4,
      price: 978.47,
      color: 'from-[#d4a853] to-[#b8923f]',
      bgColor: 'bg-amber-50',
      borderColor: 'border-amber-200',
      popular: true,
      description: '4 sterren hotels incl. ontbijt, voor elke bestemming 1 activiteit',
      breakdown: [
        { item: 'Vlucht', price: 322.97 },
        { item: 'Hotels', price: 523.00 },
        { item: 'Vervoer', price: 69.00 },
        { item: 'Activiteit', price: 63.50 }
      ],
      includes: [
        'Vlucht heen en terug',
        '4★ hotels met ontbijt',
        'Vervoer tussen bestemmingen',
        '1 activiteit per bestemming'
      ]
    },
    {
      id: 'ultra',
      name: 'Ultra',
      tagline: 'Het duurste pakket',
      stars: 5,
      price: 2186.47,
      color: 'from-purple-600 to-purple-900',
      bgColor: 'bg-purple-50',
      borderColor: 'border-purple-200',
      description: '5 sterrenhotel, incl. ontbijt en diner',
      breakdown: [
        { item: 'Vlucht', price: 322.97 },
        { item: 'Hotels', price: 1592.00 },
        { item: 'Vervoer', price: 69.00 },
        { item: 'Activiteiten', price: 202.50 }
      ],
      includes: [
        'Vlucht heen en terug',
        '5★ luxe hotels',
        'Ontbijt én diner inbegrepen',
        'Vervoer tussen bestemmingen',
        '2 activiteiten bij 2 bestemmingen'
      ]
    }
  ];

  const handleBook = (pkg) => {
    setSelectedPackage(pkg);
    setShowBooking(true);
  };

  return (
    <div className="min-h-screen bg-[#faf9f6]">
      {/* Hero */}
      <section className="relative py-32 px-6 bg-gradient-to-br from-[#1e3a5f] to-[#152a45] overflow-hidden">
        <div className="absolute inset-0 opacity-10">
          <div className="absolute top-20 left-20 w-72 h-72 bg-[#d4a853] rounded-full blur-3xl" />
          <div className="absolute bottom-20 right-20 w-96 h-96 bg-[#e07a5f] rounded-full blur-3xl" />
        </div>
        <div className="max-w-7xl mx-auto text-center relative z-10">
          <motion.div
            initial={{ opacity: 0, y: 20 }}
            animate={{ opacity: 1, y: 0 }}
          >
            <span className="inline-block px-4 py-2 bg-[#d4a853]/20 rounded-full text-[#d4a853] text-sm font-medium mb-6">
              29 mei - 8 juni 2025
            </span>
            <h1 className="text-5xl md:text-6xl font-bold text-white mb-6">
              Kies je Pakket
            </h1>
            <p className="text-xl text-white/70 max-w-2xl mx-auto">
              Selecteer het pakket dat bij jou past. Van budget tot luxe, 
              allemaal inclusief vlucht, hotels en vervoer.
            </p>
          </motion.div>
        </div>
      </section>

      {/* Packages Grid */}
      <section className="py-24 px-6 -mt-16">
        <div className="max-w-7xl mx-auto">
          <div className="grid lg:grid-cols-3 gap-8">
            {packages.map((pkg, index) => (
              <motion.div
                key={pkg.id}
                className={`relative rounded-3xl ${pkg.bgColor} border-2 ${pkg.borderColor} overflow-hidden`}
                initial={{ opacity: 0, y: 30 }}
                animate={{ opacity: 1, y: 0 }}
                transition={{ delay: index * 0.15 }}
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
            initial={{ opacity: 0, y: 20 }}
            whileInView={{ opacity: 1, y: 0 }}
            viewport={{ once: true }}
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
                initial={{ opacity: 0, y: 20 }}
                whileInView={{ opacity: 1, y: 0 }}
                transition={{ delay: index * 0.1 }}
                viewport={{ once: true }}
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
    </div>
  );
}
