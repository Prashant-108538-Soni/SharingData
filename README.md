import 'package:flutter/material.dart';
import 'package:flutter_svg/flutter_svg.dart';
import 'package:hdfc_flutter_widgets/event_card/common/description.dart';

/// Displays the primary detail row for an event or bill.
///
/// Includes:
/// - A leading circular icon (SVG)
/// - Title (e.g., "Mom's Phone Bill")
/// - Subtitle (e.g., masked account or plan)
/// - Description widget (icon + text)
class PrimaryDetail extends StatelessWidget {
  /// Path to the SVG icon shown at the start.
  final String prefixIconPath;

  /// Background color for the circular icon container.
  final Color prefixIconBackgroundColor;

  /// Main title text.
  final String title;

  /// Supporting subtitle text (e.g., account details).
  final String subtitle;

  /// Text shown in the status row.
  final String descriptionText;

  /// Path to the SVG icon used in the status row.
  final String descriptionIconPath;

  const PrimaryDetail({
    super.key,
    required this.title,
    required this.prefixIconPath,
    required this.prefixIconBackgroundColor,
    required this.descriptionIconPath,
    required this.descriptionText,
    required this.subtitle,
  });

  @override
  Widget build(BuildContext context) {
    return Row(
      crossAxisAlignment: CrossAxisAlignment.start,
      children: [
        // Leading icon inside colored circle
        Container(
          padding: const EdgeInsets.all(8),
          decoration: BoxDecoration(
            shape: BoxShape.circle,
            color: prefixIconBackgroundColor,
          ),
          alignment: Alignment.center,
          child: SizedBox(
            width: 24,
            height: 24,
            child: SvgPicture.asset(
              prefixIconPath,
              placeholderBuilder: (_) =>
                  const Icon(Icons.error_outline, color: Colors.red),
            ),
          ),
        ),

        const SizedBox(width: 12),

        // Text section
        Expanded(
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
              // Title
              Text(
                title,
                style: const TextStyle(
                  fontWeight: FontWeight.w600,
                  color: Colors.black87,
                ),
              ),

              const SizedBox(height: 4),

              // Subtitle
              Text(
                subtitle,
                style: TextStyle(
                  color: Colors.grey.shade800,
                ),
              ),

              const SizedBox(height: 20),

              // Status (icon + label)
              Description(
                svgPath: descriptionIconPath,
                text: descriptionText,
              ),
            ],
          ),
        ),
      ],
    );
  }
}