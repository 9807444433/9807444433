// File: data.js export const vendors = [ { id: 1, name: "Sharma Electronics", area: "Sigra", phone: "9801234567" }, { id: 2, name: "Lanka Mobiles", area: "Lanka", phone: "9802345678" }, ];

export const products = [ { id: 1, name: "Samsung Galaxy A14", price: 13499, vendorId: 1 }, { id: 2, name: "LG 1.5 Ton AC", price: 29999, vendorId: 2 }, ];

export const orders = [ { id: 101, product: "Samsung Galaxy A14", buyer: "Rahul", address: "Sigra, Varanasi", deliveryKm: 2 }, { id: 102, product: "LG AC", buyer: "Neha", address: "Lanka, Varanasi", deliveryKm: 5 }, ];

// File: store/useOLMStore.js import { create } from 'zustand'; import { vendors, products, orders } from '../data';

export const useOLMStore = create((set) => ({ vendors, products, orders, addProduct: (newProduct) => set((state) => ({ products: [...state.products, newProduct] })), addOrder: (newOrder) => set((state) => ({ orders: [...state.orders, newOrder] })), }));

// File: components/MobileDrawer.js import * as Dialog from '@radix-ui/react-dialog'; import { Menu } from 'lucide-react';

export default function MobileDrawer() { return ( <Dialog.Root> <Dialog.Trigger className="sm:hidden p-2"> <Menu className="w-6 h-6" /> </Dialog.Trigger> <Dialog.Overlay className="fixed inset-0 bg-black/40" /> <Dialog.Content className="fixed left-0 top-0 w-64 h-full bg-white p-4 shadow-xl space-y-4"> <Dialog.Close className="text-right w-full">❌</Dialog.Close> <div className="text-lg font-bold">OLM Menu</div> <a href="#buyer">Buyer</a> <a href="#seller">Seller</a> <a href="#delivery">Delivery</a> <a href="#admin">Admin</a> </Dialog.Content> </Dialog.Root> ); }

// File: OLMApp.jsx import React from 'react'; import { Card, CardContent } from '@/components/ui/card'; import { Button } from '@/components/ui/button'; import { Input } from '@/components/ui/input'; import { Tabs, TabsContent, TabsList, TabsTrigger } from '@/components/ui/tabs'; import { useOLMStore } from './store/useOLMStore'; import MobileDrawer from './components/MobileDrawer';

export default function OLMApp() { const products = useOLMStore((state) => state.products); const orders = useOLMStore((state) => state.orders);

return ( <div className="min-h-screen bg-gray-50 p-4"> <div className="flex justify-between items-center"> <h1 className="text-3xl font-bold mb-4 text-center sm:text-left">OLM App Interface</h1> <MobileDrawer /> </div>

<Tabs defaultValue="buyer" className="w-full max-w-4xl mx-auto">
    <TabsList className="grid grid-cols-4 gap-2">
      <TabsTrigger value="buyer">Buyer</TabsTrigger>
      <TabsTrigger value="seller">Seller</TabsTrigger>
      <TabsTrigger value="delivery">Delivery</TabsTrigger>
      <TabsTrigger value="admin">Admin</TabsTrigger>
    </TabsList>

    <TabsContent value="buyer">
      <Card id="buyer">
        <CardContent className="p-4 space-y-4">
          <Input placeholder="Search for local products..." />
          <Button className="w-full">Search</Button>
          <div className="text-sm text-gray-500">Browse deals from your local market.</div>
          <ul className="list-disc ml-4">
            {products.map((product) => (
              <li key={product.id}>{product.name} – ₹{product.price}</li>
            ))}
          </ul>
        </CardContent>
      </Card>
    </TabsContent>

    <TabsContent value="seller">
      <Card id="seller">
        <CardContent className="p-4 space-y-4">
          <Input placeholder="Add a new product" />
          <Button className="w-full">Add Product</Button>
          <div className="text-sm text-gray-500">Manage your inventory and see your orders.</div>
        </CardContent>
      </Card>
    </TabsContent>

    <TabsContent value="delivery">
      <Card id="delivery">
        <CardContent className="p-4 space-y-4">
          <div className="text-sm font-semibold">Today's Deliveries</div>
          <ul className="list-disc ml-4 text-gray-700">
            {orders.map((order) => (
              <li key={order.id}>{order.product} – {order.deliveryKm}km</li>
            ))}
          </ul>
        </CardContent>
      </Card>
    </TabsContent>

    <TabsContent value="admin">
      <Card id="admin">
        <CardContent className="p-4 space-y-4">
          <div className="text-sm">Platform Analytics</div>
          <Button>Generate Report</Button>
        </CardContent>
      </Card>
    </TabsContent>
  </Tabs>
</div>

); }

![file_000000002a4861f9b26ce823b0fd7f1d](https://github.com/user-attachments/assets/d225dbfd-d9b3-4594-b07c-61ca4c5e8b47)
