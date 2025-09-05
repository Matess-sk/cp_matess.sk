import React, { useMemo, useState } from "react";
import { Card, CardContent, CardHeader, CardTitle } from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Label } from "@/components/ui/label";
import { Switch } from "@/components/ui/switch";
import { Slider } from "@/components/ui/slider";
import { Select, SelectContent, SelectItem, SelectTrigger, SelectValue } from "@/components/ui/select";
import { Textarea } from "@/components/ui/textarea";
import { Button } from "@/components/ui/button";
import { Badge } from "@/components/ui/badge";
import { Tabs, TabsContent, TabsList, TabsTrigger } from "@/components/ui/tabs";
import { Tooltip, TooltipContent, TooltipProvider, TooltipTrigger } from "@/components/ui/tooltip";
import { Info, Percent, Calculator, Download } from "lucide-react";

// Pomocné typy
type Currency = "EUR" | "USD" | "CZK";

const CURRENCY_SYMBOL: Record<Currency, string> = { EUR: "€", USD: "$", CZK: "Kč" };
const FX: Record<Currency, number> = { EUR: 1, USD: 1.1, CZK: 25 }; // jednoduchý prepočet, uprav podľa potreby

// Základné sadzby/koeficienty – uprav podľa tvojho trhu
const COEFS = {
  dizajn: { basic: 1, custom: 1.25, premium: 1.6 },
  cms: { none: 0, wp: 0.25, headless: 0.5 },
  eshop: { none: 0, simple: 0.5, advanced: 1.1 },
  seo: { none: 0, basic: 0.15, pro: 0.35 },
  multilangPerLang: 0.12,
  accessibility: 0.12,
  performance: 0.1,
};

// Utility
const fmt = (n: number, c: Currency) => new Intl.NumberFormat("sk-SK", { style: "currency", currency: c }).format(n);

// Hlavný komponent
export default function WebPricingCalculator() {
  const [currency, setCurrency] = useState<Currency>("EUR");
  const [hourly, setHourly] = useState(35); // €/h
  const [baseHours, setBaseHours] = useState(20); // základné hodiny pre projekt
  const [pages, setPages] = useState(6);
  const [complexity, setComplexity] = useState(1.1); // násobok

  const [design, setDesign] = useState<"basic" | "custom" | "premium">("custom");
  const [cms, setCms] = useState<"none" | "wp" | "headless">("wp");
  const [eshop, setEshop] = useState<"none" | "simple" | "advanced">("none");
  const [seo, setSeo] = useState<"none" | "basic" | "pro">("basic");

  const [multilang, setMultilang] = useState(1); // počet jazykov
  const [accessibility, setAccessibility] = useState(true);
  const [performance, setPerformance] = useState(true);

  const [customFeatures, setCustomFeatures] = useState<string>(""); // CSV: "názov:hodiny"

  const [maintenanceMonthly, setMaintenanceMonthly] = useState(0); // €/mes
  const [hostingMonthly, setHostingMonthly] = useState(0); // €/mes

  const [rush, setRush] = useState(0); // % prirážka
  const [discount, setDiscount] = useState(0); // % zľava
  const [vat, setVat] = useState(0); // % DPH

  // Parsovanie vlastných funkcií: riadky "nazov:hodiny"
  const parsedFeatures = useMemo(() => {
    const rows = customFeatures
      .split(/\n|,/)
      .map((s) => s.trim())
      .filter(Boolean);
    const out: { name: string; hours: number }[] = [];
    for (const r of rows) {
      const [name, h] = r.split(":");
      const hours = Number((h ?? "0").replace(",", "."));
      if (name && !isNaN(hours) && hours > 0) out.push({ name: name.trim(), hours });
    }
    return out;
  }, [customFeatures]);

  // Výpočet hodín
  const hoursBreakdown = useMemo(() => {
    const hBase = baseHours * complexity;
    const hPages = Math.max(0, pages - 1) * 2 * complexity; // 2h na podstránku

    const hDesign = hBase * (COEFS.dizajn[design] - 1);
    const hCms = hBase * COEFS.cms[cms];
    const hShop = hBase * COEFS.eshop[eshop];
    const hSeo = hBase * COEFS.seo[seo];
    const hI18n = multilang > 1 ? hBase * COEFS.multilangPerLang * (multilang - 1) : 0;
    const hA11y = accessibility ? hBase * COEFS.accessibility : 0;
    const hPerf = performance ? hBase * COEFS.performance : 0;

    const hCustom = parsedFeatures.reduce((a, b) => a + b.hours, 0);

    const subtotalHours = hBase + hPages + hDesign + hCms + hShop + hSeo + hI18n + hA11y + hPerf + hCustom;

    return {
      hBase,
      hPages,
      hDesign,
      hCms,
      hShop,
      hSeo,
      hI18n,
      hA11y,
      hPerf,
      hCustom,
      subtotalHours,
    } as const;
  }, [baseHours, complexity, pages, design, cms, eshop, seo, multilang, accessibility, performance, parsedFeatures]);

  // Výpočet cien
  const price = useMemo(() => {
    const rate = hourly * FX[currency];
    const subtotal = hoursBreakdown.subtotalHours * rate;
    const rushAmt = subtotal * (rush / 100);
    const discountAmt = subtotal * (discount / 100);
    const oneOff = Math.max(0, subtotal + rushAmt - discountAmt);

    const monthly = (maintenanceMonthly + hostingMonthly) * FX[currency];
    const vatAmt = vat > 0 ? oneOff * (vat / 100) : 0;

    const total = oneOff + vatAmt;

    return { rate, subtotal, rushAmt, discountAmt, oneOff, monthly, vatAmt, total } as const;
  }, [hourly, currency, hoursBreakdown.subtotalHours, rush, discount, maintenanceMonthly, hostingMonthly, vat]);

  const reset = () => {
    setCurrency("EUR");
    setHourly(35);
    setBaseHours(20);
    setPages(6);
    setComplexity(1.1);
    setDesign("custom");
    setCms("wp");
    setEshop("none");
    setSeo("basic");
    setMultilang(1);
    setAccessibility(true);
    setPerformance(true);
    setCustomFeatures("");
    setMaintenanceMonthly(0);
    setHostingMonthly(0);
    setRush(0);
    setDiscount(0);
    setVat(0);
  };

  const exportJSON = () => {
    const data = {
      currency,
      hourly,
      baseHours,
      pages,
      complexity,
      design,
      cms,
      eshop,
      seo,
      multilang,
      accessibility,
      performance,
      customFeatures: parsedFeatures,
      maintenanceMonthly,
      hostingMonthly,
      rush,
      discount,
      vat,
      hoursBreakdown,
      price,
    };
    const blob = new Blob([JSON.stringify(data, null, 2)], { type: "application/json" });
    const url = URL.createObjectURL(blob);
    const a = document.createElement("a");
    a.href = url;
    a.download = `kalkulacka-ceny-webu-${Date.now()}.json`;
    a.click();
    URL.revokeObjectURL(url);
  };

  return (
    <TooltipProvider>
      <div className="min-h-screen bg-gradient-to-b from-slate-50 to-white p-6 md:p-10">
        <div className="mx-auto max-w-6xl space-y-6">
          <header className="flex flex-col gap-3 md:flex-row md:items-end md:justify-between">
            <div>
              <h1 className="text-3xl font-bold tracking-tight">Kalkulačka ceny webu</h1>
              <p className="text-slate-600">Jednoduché plánovanie nákladov na tvorbu webstránky.</p>
            </div>
            <div className="flex items-center gap-3">
              <Select value={currency} onValueChange={(v: Currency) => setCurrency(v)}>
                <SelectTrigger className="w-[120px]"><SelectValue placeholder="Mena" /></SelectTrigger>
                <SelectContent>
                  <SelectItem value="EUR">EUR</SelectItem>
                  <SelectItem value="USD">USD</SelectItem>
                  <SelectItem value="CZK">CZK</SelectItem>
                </SelectContent>
              </Select>
              <Button variant="secondary" onClick={reset}>Reset</Button>
              <Button onClick={exportJSON}><Download className="mr-2 h-4 w-4"/>Export</Button>
            </div>
          </header>

          <div className="grid grid-cols-1 gap-6 lg:grid-cols-3">
            {/* ĽAVÝ STĹPEC: vstupy */}
            <div className="lg:col-span-2 space-y-6">
              <Card className="shadow-sm">
                <CardHeader>
                  <CardTitle>Základ projektu</CardTitle>
                </CardHeader>
                <CardContent className="grid grid-cols-1 gap-4 md:grid-cols-2">
                  <div>
                    <Label>Hodinová sadzba</Label>
                    <div className="flex items-center gap-2">
                      <Input type="number" value={hourly} onChange={(e) => setHourly(Number(e.target.value))} />
                      <Badge variant="outline">{CURRENCY_SYMBOL[currency]}/h</Badge>
                    </div>
                  </div>
                  <div>
                    <Label>Základné hodiny</Label>
                    <Input type="number" value={baseHours} onChange={(e) => setBaseHours(Number(e.target.value))} />
                  </div>
                  <div>
                    <Label>Počet podstránok</Label>
                    <Input type="number" value={pages} onChange={(e) => setPages(Number(e.target.value))} />
                  </div>
                  <div>
                    <Label>Komplexita
                      <Tooltip>
                        <TooltipTrigger asChild>
                          <Info className="ml-2 inline h-4 w-4 text-slate-500" />
                        </TooltipTrigger>
                        <TooltipContent>Koeficient 1.0 = bežné, 1.5 = náročné</TooltipContent>
                      </Tooltip>
                    </Label>
                    <div className="px-1">
                      <Slider value={[complexity]} min={0.8} max={1.8} step={0.05} onValueChange={(v) => setComplexity(v[0])} />
                      <div className="mt-1 text-sm text-slate-600">{complexity.toFixed(2)}×</div>
                    </div>
                  </div>
                  <div>
                    <Label>Dizajn</Label>
                    <Select value={design} onValueChange={(v: any) => setDesign(v)}>
                      <SelectTrigger><SelectValue /></SelectTrigger>
                      <SelectContent>
                        <SelectItem value="basic">Šablónový</SelectItem>
                        <SelectItem value="custom">Na mieru</SelectItem>
                        <SelectItem value="premium">Prémiový</SelectItem>
                      </SelectContent>
                    </Select>
                  </div>
                  <div>
                    <Label>CMS</Label>
                    <Select value={cms} onValueChange={(v: any) => setCms(v)}>
                      <SelectTrigger><SelectValue /></SelectTrigger>
                      <SelectContent>
                        <SelectItem value="none">Bez CMS</SelectItem>
                        <SelectItem value="wp">WordPress</SelectItem>
                        <SelectItem value="headless">Headless</SelectItem>
                      </SelectContent>
                    </Select>
                  </div>
                  <div>
                    <Label>E‑shop</Label>
                    <Select value={eshop} onValueChange={(v: any) => setEshop(v)}>
                      <SelectTrigger><SelectValue /></SelectTrigger>
                      <SelectContent>
                        <SelectItem value="none">Bez e‑shopu</SelectItem>
                        <SelectItem value="simple">Jednoduchý</SelectItem>
                        <SelectItem value="advanced">Pokročilý</SelectItem>
                      </SelectContent>
                    </Select>
                  </div>
                  <div>
                    <Label>SEO balík</Label>
                    <Select value={seo} onValueChange={(v: any) => setSeo(v)}>
                      <SelectTrigger><SelectValue /></SelectTrigger>
                      <SelectContent>
                        <SelectItem value="none">Žiadny</SelectItem>
                        <SelectItem value="basic">Základ</SelectItem>
                        <SelectItem value="pro">Pro</SelectItem>
                      </SelectContent>
                    </Select>
                  </div>
                  <div>
                    <Label>Počet jazykov</Label>
                    <Input type="number" value={multilang} onChange={(e) => setMultilang(Math.max(1, Number(e.target.value)))} />
                  </div>
                  <div className="flex items-center gap-3 pt-6">
                    <Switch checked={accessibility} onCheckedChange={setAccessibility} />
                    <Label>Prístupnosť (WCAG)</Label>
                  </div>
                  <div className="flex items-center gap-3 pt-6">
                    <Switch checked={performance} onCheckedChange={setPerformance} />
                    <Label>Výkon a optimalizácia</Label>
                  </div>
                </CardContent>
              </Card>

              <Card className="shadow-sm">
                <CardHeader>
                  <CardTitle>Vlastné funkcionality</CardTitle>
                </CardHeader>
                <CardContent>
                  <Label>Každý riadok vo formáte <code>nazov:hodiny</code></Label>
                  <Textarea
                    rows={5}
                    placeholder={`Rezervácie:10\nNapojenie na CRM:6\nPlatobná brána:4`}
                    value={customFeatures}
                    onChange={(e) => setCustomFeatures(e.target.value)}
                  />
                </CardContent>
              </Card>

              <Card className="shadow-sm">
                <CardHeader>
                  <CardTitle>Prevádzka a podmienky</CardTitle>
                </CardHeader>
                <CardContent className="grid grid-cols-1 gap-4 md:grid-cols-3">
                  <div>
                    <Label>Údržba mesačne</Label>
                    <Input type="number" value={maintenanceMonthly} onChange={(e) => setMaintenanceMonthly(Number(e.target.value))} />
                  </div>
                  <div>
                    <Label>Hosting mesačne</Label>
                    <Input type="number" value={hostingMonthly} onChange={(e) => setHostingMonthly(Number(e.target.value))} />
                  </div>
                  <div>
                    <Label><Percent className="mr-1 inline h-4 w-4"/>DPH (%)</Label>
                    <Input type="number" value={vat} onChange={(e) => setVat(Math.max(0, Number(e.target.value)))} />
                  </div>
                  <div>
                    <Label>Prirážka za urgentnosť (%)</Label>
                    <Input type="number" value={rush} onChange={(e) => setRush(Math.max(0, Number(e.target.value)))} />
                  </div>
                  <div>
                    <Label>Zľava (%)</Label>
                    <Input type="number" value={discount} onChange={(e) => setDiscount(Math.max(0, Number(e.target.value)))} />
                  </div>
                </CardContent>
              </Card>
            </div>

            {/* PRAVÝ STĹPEC: výsledok */}
            <div className="space-y-6">
              <Card className="sticky top-6 shadow-md">
                <CardHeader className="pb-2">
                  <div className="flex items-center justify-between">
                    <CardTitle>Odhad ceny</CardTitle>
                    <Badge variant="secondary"><Calculator className="mr-1 h-4 w-4"/>{hoursBreakdown.subtotalHours.toFixed(1)} h</Badge>
                  </div>
                </CardHeader>
                <CardContent className="space-y-3">
                  <div className="text-3xl font-bold tracking-tight">{fmt(price.total, currency)}</div>
                  <div className="text-sm text-slate-600">Bez DPH: {fmt(price.oneOff, currency)} • Sadzba: {fmt(price.rate, currency)}/h</div>
                  {price.monthly > 0 && (
                    <div className="text-sm text-slate-600">Mesačne: {fmt(price.monthly, currency)}</div>
                  )}

                  <Tabs defaultValue="rozpis" className="mt-2">
                    <TabsList>
                      <TabsTrigger value="rozpis">Rozpis</TabsTrigger>
                      <TabsTrigger value="hodiny">Hodiny</TabsTrigger>
                    </TabsList>
                    <TabsContent value="rozpis" className="space-y-2 pt-2 text-sm">
                      <Row label="Medzisúčet" value={price.subtotal} currency={currency} />
                      {price.rushAmt > 0 && <Row label="Prirážka za urgentnosť" value={price.rushAmt} currency={currency} />}
                      {price.discountAmt > 0 && <Row label="Zľava" value={-price.discountAmt} currency={currency} />}
                      <Row label="Jednorazovo bez DPH" value={price.oneOff} currency={currency} strong />
                      {price.vatAmt > 0 && <Row label="DPH" value={price.vatAmt} currency={currency} />}
                      <Row label="Spolu" value={price.total} currency={currency} strong large />
                    </TabsContent>
                    <TabsContent value="hodiny" className="pt-2 text-sm">
                      <HoursTable breakdown={hoursBreakdown} />
                    </TabsContent>
                  </Tabs>
                </CardContent>
              </Card>

              <Card className="shadow-sm">
                <CardHeader>
                  <CardTitle>Citácia do ponuky</CardTitle>
                </CardHeader>
                <CardContent>
                  <Textarea
                    readOnly
                    value={`Odhad jednorazových nákladov: ${fmt(price.total, currency)} (${fmt(price.oneOff, currency)} bez DPH).\nPredpokladané trvanie: ${hoursBreakdown.subtotalHours.toFixed(1)} h pri sadzbe ${fmt(price.rate, currency)}/h.\nMesačné náklady: ${price.monthly > 0 ? fmt(price.monthly, currency) : "0"}.`}
                  />
                </CardContent>
              </Card>
            </div>
          </div>

          <footer className="pt-4 text-center text-xs text-slate-500">
            Model výpočtu je odhad. Uprav sadzby a koeficienty podľa reálneho projektu.
          </footer>
        </div>
      </div>
    </TooltipProvider>
  );
}

function Row({ label, value, currency, strong = false, large = false }: { label: string; value: number; currency: Currency; strong?: boolean; large?: boolean }) {
  return (
    <div className={`flex items-center justify-between ${large ? "text-base" : "text-sm"}`}>
      <span className="text-slate-600">{label}</span>
      <span className={`${strong ? "font-semibold" : ""}`}>{fmt(value, currency)}</span>
    </div>
  );
}

function HoursTable({ breakdown }: { breakdown: { [k: string]: number } }) {
  const rows = [
    ["Základ", breakdown.hBase],
    ["Podstránky", breakdown.hPages],
    ["Dizajn", breakdown.hDesign],
    ["CMS", breakdown.hCms],
    ["E‑shop", breakdown.hShop],
    ["SEO", breakdown.hSeo],
    ["Jazyky", breakdown.hI18n],
    ["Prístupnosť", breakdown.hA11y],
    ["Výkon", breakdown.hPerf],
    ["Vlastné funkcie", breakdown.hCustom],
  ].filter(([, v]) => v && v > 0.001);

  return (
    <div className="rounded-2xl border p-3">
      {rows.length === 0 ? (
        <div className="text-slate-500">Bez doplnkových hodín</div>
      ) : (
        <div className="space-y-1 text-sm">
          {rows.map(([k, v]) => (
            <div key={String(k)} className="flex items-center justify-between">
              <span className="text-slate-600">{k as string}</span>
              <span className="tabular-nums">{(v as number).toFixed(1)} h</span>
            </div>
          ))}
          <div className="mt-2 flex items-center justify-between border-t pt-2 font-semibold">
            <span>Spolu</span>
            <span className="tabular-nums">{breakdown.subtotalHours.toFixed(1)} h</span>
          </div>
        </div>
      )}
    </div>
  );
}
