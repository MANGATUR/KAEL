# KAEL
THIS WEB TRY TO THE CODING
LocationManager locationManager = (LocationManager) getSystemService(Context.LOCATION_SERVICE);
LocationListener locationListener = new LocationListener() {
    @Override
    public void onLocationChanged(Location location) {
        // Mendapatkan latitude dan longitude
        double latitude = location.getLatitude();
        double longitude = location.getLongitude();
    }

    @Override
    public void onStatusChanged(String provider, int status, Bundle extras) {

    }

    @Override
    public void onProviderEnabled(String provider) {

    }

    @Override
    public void onProviderDisabled(String provider) {

    }
};

// Permintaan update lokasi setiap 10 detik atau 10 meter
locationManager.requestLocationUpdates(LocationManager.GPS_PROVIDER, 10000, 10, locationListener);

// Mendapatkan referensi dari fragment atau layout yang akan digunakan untuk menampilkan peta
SupportMapFragment mapFragment = (SupportMapFragment) getSupportFragmentManager().findFragmentById(R.id.map);
mapFragment.getMapAsync(new OnMapReadyCallback() {
    @Override
    public void onMapReady(GoogleMap googleMap) {
        // Menambahkan marker pada lokasi saat ini
        googleMap.addMarker(new MarkerOptions().position(new LatLng(latitude, longitude)).title("Lokasi saat ini"));
        // Memindahkan kamera ke lokasi saat ini
        googleMap.moveCamera(CameraUpdateFactory.newLatLng(new LatLng(latitude, longitude)));
    }
});
