echo "# henzem" >> README.md

Dokumen Persyaratan Produk (PRD) - Proyek Henzem
Platform Trading Ekspor Agrikultur D2C/B2B Berbasis Cloud
Versi: 2.0 (Final Version)
Tanggal: 15 Juni 2026
Status: Approved / Siap Implementasi
Stack Teknis Utama: Next.js (App Router) + Convex.dev
Target Rilis MVP: 1 - 3 Bulan

1. Ringkasan Eksekutif & Visi Produk
1.1 Latar Belakang
Indonesia memiliki potensi agrikultur dan hasil bumi yang luar biasa besar (kopi, rempah-rempah, kelapa, dll.). Namun, kontribusi UMKM terhadap ekspor nasional masih di bawah 20%. Kendala utama yang dihadapi oleh UMKM agrikultur meliputi rumitnya birokrasi dokumen, kurangnya akses langsung ke pembeli global (Buyer), serta ketakutan akan risiko transaksi lintas negara.
1.2 Visi Henzem
Henzem hadir sebagai platform Direct-to-Consumer (D2C) dan Business-to-Business (B2B) ekspor yang menjembatani UMKM Agrikultur Indonesia langsung dengan pembeli global. Henzem memadukan efisiensi teknologi modern (Next.js + Convex) dengan pendekatan "High-Touch" (Pendampingan Manusia) melalui peran Account Manager (AM) internal untuk mengedukasi dan mengawal proses ekspor hingga selesai.
1.3 Model Bisnis Utama
Model Transaksi: Berbasis Request for Quotation (RFQ). Buyer memposting kebutuhan, Seller (SME) mengajukan penawaran (bidding).
Monetisasi: Komisi persentase (%) dari setiap nilai transaksi yang berhasil dikonfirmasi + komisi agen (brokerage) dari integrasi asuransi kargo pihak ketiga.
Aliran Dana: Direct Transfer (Pembayaran langsung dari Buyer ke Seller setelah kesepakatan dicapai secara offline/WhatsApp untuk menjaga likuiditas UMKM).

2. Profil Pengguna (User Personas)
Platform Henzem membagi hak akses dan fungsionalitas sistem ke dalam 3 aktor utama:
2.1 Seller (Eksportir UMKM)
Profil: Produsen, petani, atau koperasi agrikultur skala kecil-menengah di Indonesia yang ingin melakukan ekspor tetapi awam teknologi dan regulasi.
Kebutuhan: Menemukan pembeli luar negeri yang valid, mendapatkan bimbingan pembuatan dokumen, mendapat kepastian asuransi pengiriman.
Tingkat Verifikasi: Moderat (Wajib unggah KTP/NIB dan verifikasi nomor WhatsApp).
2.2 Buyer (Importir Global)
Profil: Perusahaan skala kecil-menengah, pemilik kedai/toko, atau distributor di luar negeri yang mencari pasokan komoditas segar langsung dari tangan pertama di Indonesia.
Kebutuhan: Mendapatkan penawaran harga terbaik secara transparan, melacak status pengiriman, mendapatkan produk terkurasi.
2.3 Admin / Account Manager (AM Henzem)
Profil: Tim internal Henzem yang bertindak sebagai jembatan komunikasi, fasilitator dokumen, moderator platform, dan pengelola pendapatan (komisi).
Kebutuhan: Admin Dashboard (Super App) komprehensif untuk menyetujui KYC, memoderasi konten RFQ, memantau handover WhatsApp, menagih komisi, dan mengelola sengketa (dispute).

3. Ruang Lingkup MVP (Minimum Viable Product)
IN-SCOPE (Fase 1):
Sistem Pembuatan Akun & Profil Terverifikasi (KTP/NIB).
Papan Lowongan Kerja / Kebutuhan Barang (RFQ Board).
Sistem Pengajuan Proposal Harga (Bidding System).
Fitur Handover Otomatis ke WhatsApp setelah Bid disetujui.
Portal Unggah Dokumen Ekspor Mandiri (BL, Invoice, Packing List).
Opsi Pembelian Add-on Asuransi Kargo saat checkout bid.
Admin Dashboard Komprehensif untuk manajemen platform end-to-end.
OUT-OF-SCOPE (Fase Selanjutnya):
Integrasi Payment Gateway Multi-currency (Escrow otomatis).
Integrasi API Pelacakan Kapal kontainer real-time (misal MarineTraffic).
Chat internal di dalam platform dengan fitur auto-translation bahasa.
Integrasi otomatis dengan Sistem INSW / Bea Cukai.

4. Spesifikasi Fungsional & Fitur Inti
4.1 Modul RFQ (Request for Quotation)
Kebutuhan Data Input: Kategori Produk, Deskripsi Spesifikasi, Jumlah (Ton/Kg), Target Harga (USD), Batas Waktu.
Alur Validasi: RFQ baru berstatus pending. Harus disetujui Admin sebelum tampil di feed publik Seller (mencegah spam/konten tidak relevan).
4.2 Modul Bidding & Matchmaking
Keterbatasan Kontrol: Seller mengajukan maksimal 1 penawaran per RFQ.
Notifikasi: Buyer menerima notifikasi real-time (via Convex subscriptions) ketika bid masuk. Buyer dapat accept atau reject.
4.3 Modul Handover & Pendampingan AM (High-Touch Flow)
Saat Buyer "Accept Bid":
RFQ menjadi Closed, Transaksi menjadi Negotiating.
Sistem menugaskan 1 Account Manager internal ke transaksi.
Sistem mengenerate tautan langsung untuk komunikasi eksternal (WhatsApp/Email) antara Buyer, Seller, dan AM.
4.4 Modul Manajemen Dokumen & Asuransi
Penyimpanan Dokumen: Seller mengunggah file bukti (Invoice, Bill of Lading, Resi Pembayaran, dll) menggunakan Convex File Storage.
Asuransi: Add-on opsional. Jika dipilih, AM akan menghitung biaya asuransi secara manual dan memasukkannya ke dalam total komisi yang harus dibayar Seller.
4.5 Modul Admin Dashboard (Account Manager Portal)
Admin Dashboard adalah pusat kendali operasi Henzem. Dibangun di atas Next.js Client Components untuk interaktivitas instan. Fiturnya meliputi:
Overview / Metrik Utama: Total RFQ aktif & Pending, Total KYC menunggu verifikasi, Total Transaksi Aktif, Estimasi Komisi Tertagih.
User Management & KYC Center: Tabel daftar pengguna, fitur lihat dokumen KTP/NIB, tombol Approve/Reject.
RFQ Moderation Board: Daftar RFQ baru, fitur edit tipografi, tombol Approve/Reject.
Transaction & Document Control: Kanban Board View transaksi, akses unduh dokumen Seller.
Commission & Billing Management: Kalkulasi komisi, penanda status pembayaran komisi (Unpaid/Paid).
Dispute Resolution Center: Panel sengketa Buyer/Seller dengan internal notes admin.

5. Arsitektur Teknologi (Tech Stack)
Frontend Framework: Next.js 14/15 (App Router). Server Components untuk SEO/Landing Page, Client Components untuk Dashboard.
Styling & UI: Tailwind CSS + Shadcn/ui.
Backend & Database: Convex.dev. Skema database menggunakan TypeScript. Menggantikan REST API dengan WebSocket untuk sinkronisasi state instan antar semua Dashboard.
Autentikasi: Clerk (Login Google, Apple, Email OTP). Terhubung langsung dengan Convex Auth.
Storage: Convex File Storage (Untuk penyimpanan gambar profil, KTP, dan dokumen PDF ekspor).

6. Skema Database (Convex Schema)
import { defineSchema, defineTable } from "convex/server";
import { v } from "convex/values";

export default defineSchema({
  users: defineTable({
    clerkId: v.string(),
    name: v.string(),
    companyName: v.optional(v.string()),
    role: v.union(v.literal("buyer"), v.literal("seller"), v.literal("admin")),
    phone: v.string(),
    kycStatus: v.union(v.literal("unverified"), v.literal("pending"), v.literal("verified")),
    kycDocumentsId: v.optional(v.array(v.string())),
    createdAt: v.number(),
  }).index("by_clerkId", ["clerkId"]),

  rfqs: defineTable({
    buyerId: v.id("users"),
    productCategory: v.string(),
    title: v.string(),
    description: v.string(),
    quantity: v.string(),
    targetPrice: v.string(), // USD
    status: v.union(v.literal("pending_moderation"), v.literal("open"), v.literal("closed"), v.literal("rejected")),
    createdAt: v.number(),
  }).index("by_status", ["status"]),

  bids: defineTable({
    rfqId: v.id("rfqs"),
    sellerId: v.id("users"),
    priceOffer: v.string(), // USD
    notes: v.optional(v.string()),
    insuranceRequested: v.boolean(),
    isAccepted: v.boolean(),
    createdAt: v.number(),
  }).index("by_rfqId", ["rfqId"]),

  transactions: defineTable({
    rfqId: v.id("rfqs"),
    bidId: v.id("bids"),
    buyerId: v.id("users"),
    sellerId: v.id("users"),
    adminId: v.id("users"), // Account Manager assign
    status: v.union(
      v.literal("negotiating"), 
      v.literal("paid"), 
      v.literal("shipped"), 
      v.literal("completed"), 
      v.literal("disputed")
    ),
    commissionFee: v.number(), // IDR/USD
    commissionStatus: v.union(v.literal("unpaid"), v.literal("paid")),
    internalNotes: v.optional(v.string()),
    createdAt: v.number(),
  }).index("by_adminId", ["adminId"]),

  documents: defineTable({
    transactionId: v.id("transactions"),
    uploadedBy: v.id("users"),
    docType: v.union(v.literal("invoice"), v.literal("bill_of_lading"), v.literal("payment_receipt"), v.literal("other")),
    fileStorageId: v.string(),
    createdAt: v.number(),
  }),
});
      

7. Diagram Alur Sistem (User Flows) Termasuk Admin
Alur Matchmaking & Penugasan Admin
[Buyer] --(Buat RFQ)--> [Status: Pending]
                             |
                      [Admin Dashboard] --(Review & Approve)--> [Status: Open]
                             |
[Seller] --(Lihat & Kirim Bid)--> [Proposal Harga Terkirim]
                             |
[Buyer] --(Accept Bid)--> [RFQ Closed, Transaksi Dibuat]
                             |
                      [Admin Dashboard] --(Auto-Assign AM)--> [Buka Akses Kontak WhatsApp]
      
Alur Transaksi & Admin Control
[Proses Offline via WhatsApp Didampingi AM]
                             |
[Buyer Transfer & Seller Upload Resi di Portal] --> [Status: Paid]
                             |
[Seller Ekspor & Upload B/L di Portal] --> [Status: Shipped]
                             |
                      [Admin Dashboard] --(Validasi Dokumen & Generate Tagihan Komisi)
                             |
[Seller Bayar Komisi ke Henzem] --> [Admin Update Commission = Paid]
                             |
[Buyer Konfirmasi Terima Barang & Rating] --> [Status: Completed]
      

8. Protokol Keamanan, Kepercayaan & Sengketa
Proses KYC Ketat Terpandu: Semua pendaftar Seller akan ditinjau manual lewat Admin Dashboard. Admin dapat melihat dokumen KTP/NIB dan memverifikasi nomor telepon.
Sistem Rating: Hanya aktif setelah transaksi berstatus Completed.
Dispute Management (Manajemen Sengketa): Fitur sentral di Admin Dashboard di mana AM dapat merujuk riwayat dokumen (Invoice & B/L) yang tersimpan permanen di platform sebagai alat bukti untuk mediasi.

9. Rencana Garis Waktu Pengembangan (12-Week Roadmap)
Minggu
Fokus Utama MVP
Target Deliverables
 
W1 - W2
Setup Framework & Autentikasi
Next.js, Clerk, Convex Config, Schema DB Setup, Auth UI.
W3 - W4
Core User Management
Seller/Buyer Dashboard, Profiling, Form KYC (Upload via Convex).
W5 - W6
Admin Dashboard Core
Panel KYC Approval, RFQ Moderation Panel, Summary Analytics.
W7 - W8
RFQ & Bidding Engine
Form Buat RFQ, RFQ Feed Page, Fitur Bidding dengan Reactive UI.
W9 - W10
Logika Handover & Transaksi
Flow "Accept Bid", Auto-Assign Admin, Kanban Board Transaksi di Admin Portal, Modul Upload Dokumen Ekspor.
W11
UAT & Final Review
Testing end-to-end, Perbaikan UX Dashboard Admin.
W12
Go-Live
Deployment Vercel, Onboarding Admin & Pilot UMKM.


10. Matriks Keberhasilan (KPI) MVP
Liquidity Rate RFQ: > 70% RFQ mendapatkan bid dalam 48 jam.
Handover Success Rate: > 50% RFQ yang disetujui berlanjut ke komunikasi aktif didampingi AM.
Admin Efficiency (SLA): Rata-rata waktu verifikasi KYC dan persetujuan RFQ oleh admin berada di bawah 2 jam kerja.
Commission Collection Rate: > 90% komisi dari transaksi shipped/completed berhasil ditagih oleh tim Admin.
